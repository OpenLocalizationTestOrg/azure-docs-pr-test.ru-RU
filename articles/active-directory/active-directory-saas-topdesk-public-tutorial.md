---
title: "Руководство. Интеграция Azure Active Directory с TOPdesk - Public | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="18d89-103">Учебник. Интеграция Azure Active Directory с TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="18d89-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="18d89-104">В этом руководстве описано, как интегрировать TOPdesk - Public с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18d89-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18d89-105">Интеграция Azure AD с приложением TOPdesk - Public обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="18d89-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18d89-106">C помощью Azure AD вы можете контролировать доступ к TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="18d89-107">Вы можете включить автоматический вход пользователей в TOPdesk - Public (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18d89-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="18d89-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="18d89-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="18d89-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18d89-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18d89-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18d89-110">Prerequisites</span></span>

<span data-ttu-id="18d89-111">Чтобы настроить интеграцию Azure AD с TOPdesk - Public, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="18d89-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="18d89-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="18d89-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18d89-113">Подписка TOPdesk — Public с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="18d89-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18d89-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="18d89-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18d89-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="18d89-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18d89-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="18d89-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18d89-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18d89-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18d89-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="18d89-118">Scenario description</span></span>
<span data-ttu-id="18d89-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="18d89-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18d89-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="18d89-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18d89-121">Добавление TOPdesk - Public из коллекции</span><span class="sxs-lookup"><span data-stu-id="18d89-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="18d89-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18d89-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="18d89-123">Добавление TOPdesk - Public из коллекции</span><span class="sxs-lookup"><span data-stu-id="18d89-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="18d89-124">Чтобы настроить интеграцию TOPdesk - Public с Azure AD, необходимо добавить TOPdesk - Public из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="18d89-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18d89-125">**Чтобы добавить TOPdesk - Public из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="18d89-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18d89-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18d89-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="18d89-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="18d89-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18d89-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18d89-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="18d89-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="18d89-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="18d89-133">В поле поиска введите **TOPdesk - Public**, выберите **TOPdesk - Public** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="18d89-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Public в списке результатов](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="18d89-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18d89-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="18d89-136">В этом разделе описана настройка и проверка единого входа Azure AD в TOPdesk - Public с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18d89-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18d89-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в TOPdesk - Public соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18d89-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="18d89-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="18d89-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18d89-140">Чтобы настроить и проверить единый вход Azure AD в TOPdesk - Public, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="18d89-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18d89-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="18d89-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18d89-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18d89-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18d89-143">**[Создание тестового пользователя TOPdesk - Public](#create-a-topdesk---public-test-user)** требуется для того, чтобы в TOPdesk - Public существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18d89-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="18d89-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18d89-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18d89-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="18d89-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="18d89-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="18d89-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="18d89-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="18d89-148">**Чтобы настроить единый вход Azure AD в TOPdesk - Public, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="18d89-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="18d89-149">На портале Azure на странице интеграции с приложением **TOPdesk - Public** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="18d89-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="18d89-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="18d89-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="18d89-153">В разделе **Домены и URL-адреса приложения TOPdesk - Public** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="18d89-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="18d89-155">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-155">a.</span></span> <span data-ttu-id="18d89-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="18d89-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="18d89-157">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-157">b.</span></span> <span data-ttu-id="18d89-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="18d89-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="18d89-159">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-159">c.</span></span> <span data-ttu-id="18d89-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.topdesk.net/tas/public/login/saml`.</span><span class="sxs-lookup"><span data-stu-id="18d89-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="18d89-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="18d89-161">These values are not real.</span></span> <span data-ttu-id="18d89-162">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="18d89-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="18d89-163">URL-адрес ответа поясняется далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="18d89-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="18d89-164">Чтобы получить эти данные, обратитесь в [службу поддержки клиентов TOPdesk - Public](https://help.topdesk.com/saas/enterprise/user/).</span><span class="sxs-lookup"><span data-stu-id="18d89-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="18d89-165">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="18d89-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="18d89-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="18d89-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="18d89-169">В разделе **Конфигурация TOPdesk - Public** щелкните **Настройка TOPdesk - Public**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="18d89-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="18d89-170">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="18d89-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="18d89-172">Выполните вход на веб-сайт **TOPdesk — Public** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="18d89-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="18d89-173">В меню **TOPdesk** выберите пункт **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="18d89-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="18d89-174">![Параметры](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="18d89-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="18d89-175">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="18d89-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="18d89-176">![Параметры входа](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="18d89-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="18d89-177">Разверните меню **Login Settings** (Параметры входа), а затем выберите **General** (Общие).</span><span class="sxs-lookup"><span data-stu-id="18d89-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="18d89-178">![Общие](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="18d89-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="18d89-179">В разделе **Public** (Общедоступные) для конфигурации **SAML login** (Вход SAML) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="18d89-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="18d89-180">![Технические параметры](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Технические параметры")</span><span class="sxs-lookup"><span data-stu-id="18d89-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="18d89-181">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-181">a.</span></span> <span data-ttu-id="18d89-182">Нажмите кнопку **Скачать** , чтобы скачать общедоступный файл метаданных, а затем сохраните его локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="18d89-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="18d89-183">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-183">b.</span></span> <span data-ttu-id="18d89-184">Откройте скачанный файл метаданных и определите местоположение узла **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="18d89-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="18d89-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="18d89-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="18d89-186">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-186">c.</span></span> <span data-ttu-id="18d89-187">Скопируйте значение **AssertionConsumerService**, вставьте это значение в текстовое поле **URL-адрес ответа** в разделе **Домен и URL-адреса TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="18d89-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="18d89-188">Чтобы создать файл сертификата, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="18d89-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="18d89-189">![Сертификат](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Сертификат")</span><span class="sxs-lookup"><span data-stu-id="18d89-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="18d89-190">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-190">a.</span></span> <span data-ttu-id="18d89-191">Откройте скачанный файл метаданных на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="18d89-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="18d89-192">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-192">b.</span></span> <span data-ttu-id="18d89-193">Разверните узел **RoleDescriptor**, содержащий **xsi:type** со значением **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="18d89-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="18d89-194">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-194">c.</span></span> <span data-ttu-id="18d89-195">Скопируйте значение узла **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="18d89-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="18d89-196">d.</span><span class="sxs-lookup"><span data-stu-id="18d89-196">d.</span></span> <span data-ttu-id="18d89-197">Сохраните скопированное значение узла **X509Certificate** локально в файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="18d89-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="18d89-198">В разделе **Public** (Общедоступные) щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="18d89-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="18d89-199">![Вход SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Вход SAML")</span><span class="sxs-lookup"><span data-stu-id="18d89-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="18d89-200">На странице диалогового окна **Помощник настройки SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="18d89-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="18d89-201">![Помощник по настройке SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Помощник по настройке SAML")</span><span class="sxs-lookup"><span data-stu-id="18d89-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="18d89-202">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-202">a.</span></span> <span data-ttu-id="18d89-203">Чтобы отправить скачанный файл метаданных через портал Azure, напротив пункта **Federation Metadata** (Метаданные федерации) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="18d89-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="18d89-204">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-204">b.</span></span> <span data-ttu-id="18d89-205">Чтобы отправить файл сертификата, напротив пункта **Certificate (RSA)** (Сертификат (RSA)) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="18d89-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="18d89-206">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-206">c.</span></span> <span data-ttu-id="18d89-207">Чтобы отправить файл с логотипом, полученный от службы поддержки TOPdesk, напротив пункта **Logo icon** (Значок логотипа) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="18d89-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="18d89-208">d.</span><span class="sxs-lookup"><span data-stu-id="18d89-208">d.</span></span> <span data-ttu-id="18d89-209">В текстовое поле **Атрибут имени пользователя** введите значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="18d89-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="18d89-210">д.</span><span class="sxs-lookup"><span data-stu-id="18d89-210">e.</span></span> <span data-ttu-id="18d89-211">В текстовом поле **Отображаемое имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="18d89-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="18d89-212">Е.</span><span class="sxs-lookup"><span data-stu-id="18d89-212">f.</span></span> <span data-ttu-id="18d89-213">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="18d89-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="18d89-214">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="18d89-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18d89-215">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="18d89-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18d89-216">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="18d89-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="18d89-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="18d89-217">Create an Azure AD test user</span></span>

<span data-ttu-id="18d89-218">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18d89-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="18d89-220">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="18d89-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18d89-221">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18d89-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="18d89-223">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="18d89-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="18d89-225">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="18d89-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="18d89-227">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="18d89-227">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="18d89-229">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-229">a.</span></span> <span data-ttu-id="18d89-230">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18d89-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18d89-231">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-231">b.</span></span> <span data-ttu-id="18d89-232">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18d89-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="18d89-233">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-233">c.</span></span> <span data-ttu-id="18d89-234">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="18d89-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="18d89-235">г)</span><span class="sxs-lookup"><span data-stu-id="18d89-235">d.</span></span> <span data-ttu-id="18d89-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="18d89-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="18d89-237">Создание тестового пользователя TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="18d89-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="18d89-238">Чтобы пользователи Azure AD могли выполнять вход в систему TOPdesk — Public, они должны быть подготовлены для нее.</span><span class="sxs-lookup"><span data-stu-id="18d89-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="18d89-239">В случае TOPdesk — Public подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="18d89-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="18d89-240">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="18d89-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="18d89-241">Выполните вход на веб-сайт **TOPdesk — Public** своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="18d89-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="18d89-242">В меню в верхней части страницы щелкните **TOPdesk \> New \> Support Files \> Person** ("TOPdesk" > "Создать" > "Файлы поддержки" > "Пользователь").</span><span class="sxs-lookup"><span data-stu-id="18d89-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="18d89-243">![Пользователь](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="18d89-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="18d89-244">В диалоговом окне "Новый пользователь" выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="18d89-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="18d89-245">![Новый пользователь](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="18d89-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="18d89-246">а.</span><span class="sxs-lookup"><span data-stu-id="18d89-246">a.</span></span> <span data-ttu-id="18d89-247">Перейдите на вкладку "Общее".</span><span class="sxs-lookup"><span data-stu-id="18d89-247">Click the General tab.</span></span>

    <span data-ttu-id="18d89-248">b.</span><span class="sxs-lookup"><span data-stu-id="18d89-248">b.</span></span> <span data-ttu-id="18d89-249">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например Simon.</span><span class="sxs-lookup"><span data-stu-id="18d89-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="18d89-250">c.</span><span class="sxs-lookup"><span data-stu-id="18d89-250">c.</span></span> <span data-ttu-id="18d89-251">Выберите **Веб-сайт** для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="18d89-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="18d89-252">d.</span><span class="sxs-lookup"><span data-stu-id="18d89-252">d.</span></span> <span data-ttu-id="18d89-253">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="18d89-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="18d89-254">Для подготовки учетных записей Azure AD вы можете использовать любые другие инструменты или API-интерфейсы создания пользователей, предоставляемые TOPdesk — Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="18d89-255">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="18d89-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="18d89-256">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="18d89-258">**Чтобы назначить пользователя Britta Simon приложению TOPdesk - Public, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="18d89-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="18d89-259">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18d89-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="18d89-261">В списке приложений выберите **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="18d89-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![Ссылка на TOPdesk - Public в списке "Приложения"](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="18d89-263">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="18d89-263">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="18d89-265">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="18d89-265">Click **Add** button.</span></span> <span data-ttu-id="18d89-266">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="18d89-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="18d89-268">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="18d89-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18d89-269">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="18d89-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18d89-270">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="18d89-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="18d89-271">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="18d89-271">Test single sign-on</span></span>

<span data-ttu-id="18d89-272">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="18d89-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18d89-273">Щелкнув элемент TOPdesk - Public на панели доступа, вы автоматически войдете в приложение TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="18d89-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="18d89-274">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18d89-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="18d89-275">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="18d89-275">Additional resources</span></span>

* [<span data-ttu-id="18d89-276">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18d89-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18d89-277">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18d89-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

