---
title: "Руководство по интеграции Azure Active Directory с Predictix Price Reporting | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Predictix Price Reporting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 62280b205f2fd691e8c75134585172b995377311
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="93838-103">Учебник. Интеграция Azure Active Directory с Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="93838-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="93838-104">В этом учебнике описано, как интегрировать Predictix Price Reporting с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93838-104">In this tutorial, you learn how to integrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93838-105">Интеграция Azure AD с Predictix Price Reporting обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="93838-105">Integrating Predictix Price Reporting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="93838-106">С помощью Azure AD вы можете контролировать доступ к Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-106">You can control in Azure AD who has access to Predictix Price Reporting.</span></span>
- <span data-ttu-id="93838-107">Вы можете включить автоматический вход пользователей в Predictix Price Reporting (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93838-107">You can enable your users to automatically get signed-on to Predictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="93838-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="93838-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="93838-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93838-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93838-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="93838-110">Prerequisites</span></span>

<span data-ttu-id="93838-111">Чтобы настроить интеграцию Azure AD с Predictix Price Reporting, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="93838-111">To configure Azure AD integration with Predictix Price Reporting, you need the following items:</span></span>

- <span data-ttu-id="93838-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="93838-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93838-113">подписка Predictix Price Reporting с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="93838-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93838-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="93838-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93838-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="93838-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93838-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="93838-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93838-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93838-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93838-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="93838-118">Scenario description</span></span>
<span data-ttu-id="93838-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="93838-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93838-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="93838-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93838-121">Добавление приложения Predictix Price Reporting из коллекции</span><span class="sxs-lookup"><span data-stu-id="93838-121">Adding Predictix Price Reporting from the gallery</span></span>
2. <span data-ttu-id="93838-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="93838-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-the-gallery"></a><span data-ttu-id="93838-123">Добавление приложения Predictix Price Reporting из коллекции</span><span class="sxs-lookup"><span data-stu-id="93838-123">Adding Predictix Price Reporting from the gallery</span></span>
<span data-ttu-id="93838-124">Чтобы настроить интеграцию Predictix Price Reporting с Azure AD, необходимо добавить приложение Predictix Price Reporting из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="93838-124">To configure the integration of Predictix Price Reporting into Azure AD, you need to add Predictix Price Reporting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93838-125">**Чтобы добавить Predictix Price Reporting из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="93838-125">**To add Predictix Price Reporting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93838-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93838-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="93838-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="93838-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="93838-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="93838-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="93838-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="93838-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="93838-133">В поле поиска введите **Predictix Price Reporting**, выберите **Predictix Price Reporting** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="93838-133">In the search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix Price Reporting в списке результатов](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="93838-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="93838-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="93838-136">В этом разделе описана настройка и проверка единого входа Azure AD в Predictix Price Reporting с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93838-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93838-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Predictix Price Reporting соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93838-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Price Reporting is to a user in Azure AD.</span></span> <span data-ttu-id="93838-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Price Reporting needs to be established.</span></span>

<span data-ttu-id="93838-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-139">In Predictix Price Reporting, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="93838-140">Чтобы настроить и проверить единый вход Azure AD в Predictix Price Reporting, вам потребуется выполнить действия в приведенных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="93838-140">To configure and test Azure AD single sign-on with Predictix Price Reporting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93838-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="93838-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93838-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93838-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93838-143">**[Создание тестового пользователя Predictix Price Reporting](#create-a-predictix-price-reporting-test-user)** требуется для создания в Predictix Price Reporting пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93838-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Price Reporting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="93838-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93838-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93838-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="93838-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="93838-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="93838-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="93838-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="93838-148">**Чтобы настроить единый вход Azure AD в Predictix Price Reporting, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="93838-148">**To configure Azure AD single sign-on with Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="93838-149">На портале Azure на странице интеграции с приложением **Predictix Price Reporting** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="93838-149">In the Azure portal, on the **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="93838-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="93838-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="93838-153">В разделе **Домены и URL-адреса приложения Predictix Price Reporting** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="93838-153">On the **Predictix Price Reporting Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="93838-155">а.</span><span class="sxs-lookup"><span data-stu-id="93838-155">a.</span></span> <span data-ttu-id="93838-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="93838-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="93838-157">b.</span><span class="sxs-lookup"><span data-stu-id="93838-157">b.</span></span> <span data-ttu-id="93838-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="93838-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="93838-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="93838-159">These values are not real.</span></span> <span data-ttu-id="93838-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="93838-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="93838-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Predictix Price Reporting](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="93838-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) to get these values.</span></span> 
 
4. <span data-ttu-id="93838-162">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="93838-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="93838-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="93838-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93838-166">В разделе **Конфигурация Predictix Price Reporting** щелкните **Настроить Predictix Price Reporting**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="93838-166">On the **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** to open **Configure sign-on** window.</span></span> <span data-ttu-id="93838-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="93838-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="93838-169">Чтобы настроить единый вход на стороне **Predictix Price Reporting**, нужно передать скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки Predictix Price Reporting](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="93838-169">To configure single sign-on on **Predictix Price Reporting** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="93838-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="93838-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="93838-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="93838-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="93838-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="93838-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="93838-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="93838-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="93838-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="93838-174">Create an Azure AD test user</span></span>

<span data-ttu-id="93838-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93838-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="93838-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="93838-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93838-178">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93838-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="93838-180">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="93838-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="93838-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="93838-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="93838-184">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="93838-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="93838-186">а.</span><span class="sxs-lookup"><span data-stu-id="93838-186">a.</span></span> <span data-ttu-id="93838-187">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93838-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93838-188">b.</span><span class="sxs-lookup"><span data-stu-id="93838-188">b.</span></span> <span data-ttu-id="93838-189">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93838-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="93838-190">c.</span><span class="sxs-lookup"><span data-stu-id="93838-190">c.</span></span> <span data-ttu-id="93838-191">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="93838-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="93838-192">г)</span><span class="sxs-lookup"><span data-stu-id="93838-192">d.</span></span> <span data-ttu-id="93838-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="93838-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="93838-194">Создание тестового пользователя Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="93838-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="93838-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="93838-196">Чтобы добавить пользователей в платформу Predictix Price Reporting, обратитесь в [службу поддержки Predictix Price Reporting](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="93838-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) to add the users in the Predictix Price Reporting platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="93838-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="93838-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="93838-198">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Price Reporting.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="93838-200">**Чтобы назначить пользователя Britta Simon приложению Predictix Price Reporting, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="93838-200">**To assign Britta Simon to Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="93838-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="93838-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="93838-203">В списке приложений выберите **Predictix Price Reporting**.</span><span class="sxs-lookup"><span data-stu-id="93838-203">In the applications list, select **Predictix Price Reporting**.</span></span>

    ![Ссылка на Predictix Price Reporting в списке приложений](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="93838-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="93838-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="93838-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="93838-207">Click **Add** button.</span></span> <span data-ttu-id="93838-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="93838-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="93838-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="93838-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="93838-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="93838-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93838-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="93838-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="93838-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="93838-213">Test single sign-on</span></span>

<span data-ttu-id="93838-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="93838-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93838-215">Щелкнув элемент Predictix Price Reporting на панели доступа, вы автоматически войдете в приложение Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="93838-215">When you click the Predictix Price Reporting tile in the Access Panel, you should get automatically signed-on to your Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93838-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="93838-216">Additional resources</span></span>

* [<span data-ttu-id="93838-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93838-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93838-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93838-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

