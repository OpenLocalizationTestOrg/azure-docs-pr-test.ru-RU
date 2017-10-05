---
title: "Руководство по интеграции Azure Active Directory с Peoplecart | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b83a1621263cac0b23bbd35a49fda213d2e4271a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="b6222-103">Руководство по интеграции Azure Active Directory с Peoplecart</span><span class="sxs-lookup"><span data-stu-id="b6222-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="b6222-104">В этом руководстве описано, как интегрировать Peoplecart с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6222-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6222-105">Интеграция Azure AD с приложением Peoplecart обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b6222-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6222-106">С помощью Azure AD вы можете контролировать доступ к Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="b6222-107">Вы можете включить автоматический вход пользователей в Peoplecart (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6222-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6222-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b6222-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6222-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6222-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6222-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6222-110">Prerequisites</span></span>

<span data-ttu-id="b6222-111">Чтобы настроить интеграцию Azure AD с Peoplecart, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b6222-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="b6222-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b6222-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6222-113">подписка Peoplecart с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6222-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6222-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b6222-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6222-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b6222-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6222-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b6222-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6222-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6222-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6222-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b6222-118">Scenario description</span></span>
<span data-ttu-id="b6222-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b6222-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6222-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b6222-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6222-121">Добавление Peoplecart из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6222-121">Adding Peoplecart from the gallery</span></span>
2. <span data-ttu-id="b6222-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6222-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="b6222-123">Добавление Peoplecart из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6222-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="b6222-124">Чтобы настроить интеграцию Peoplecart с Azure AD, необходимо добавить Peoplecart из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b6222-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6222-125">**Чтобы добавить Peoplecart из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b6222-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6222-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6222-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="b6222-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6222-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6222-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6222-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="b6222-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b6222-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="b6222-133">В поле поиска введите **Peoplecart**, выберите **Peoplecart** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="b6222-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart в списке результатов](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b6222-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6222-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b6222-136">В этом разделе описана настройка и проверка единого входа Azure AD в Peoplecart с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6222-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b6222-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Peoplecart соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6222-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="b6222-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="b6222-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6222-140">Чтобы настроить и проверить единый вход Azure AD в Peoplecart, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b6222-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6222-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b6222-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6222-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6222-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6222-143">**[Создание тестового пользователя Peoplecart](#create-a-peoplecart-test-user)** требуется для того, чтобы в Peoplecart существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6222-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6222-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6222-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6222-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b6222-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b6222-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6222-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b6222-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="b6222-148">**Чтобы настроить единый вход Azure AD в Peoplecart, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b6222-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="b6222-149">На портале Azure на странице интеграции с приложением **Peoplecart** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b6222-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b6222-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6222-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="b6222-153">В разделе **Домены и URL-адреса приложения Peoplecart** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b6222-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="b6222-155">а.</span><span class="sxs-lookup"><span data-stu-id="b6222-155">a.</span></span> <span data-ttu-id="b6222-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="b6222-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="b6222-157">b.</span><span class="sxs-lookup"><span data-stu-id="b6222-157">b.</span></span> <span data-ttu-id="b6222-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="b6222-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6222-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b6222-159">These values are not real.</span></span> <span data-ttu-id="b6222-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="b6222-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="b6222-161">Чтобы получить их, обратитесь в [службу поддержки клиентов Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6222-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
4. <span data-ttu-id="b6222-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6222-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="b6222-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b6222-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6222-166">В разделе **Конфигурация Peoplecart** щелкните **Настроить Peoplecart**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b6222-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6222-167">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b6222-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="b6222-169">Чтобы настроить единый вход на стороне **Peoplecart**, нужно отправить скачанный **XML-файл метаданных** и **URL-адрес службы единого входа SAML** [группе поддержки Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6222-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="b6222-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="b6222-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b6222-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b6222-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6222-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b6222-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6222-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b6222-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b6222-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6222-174">Create an Azure AD test user</span></span>
<span data-ttu-id="b6222-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6222-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="b6222-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b6222-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6222-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6222-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6222-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b6222-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6222-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6222-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6222-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6222-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6222-186">а.</span><span class="sxs-lookup"><span data-stu-id="b6222-186">a.</span></span> <span data-ttu-id="b6222-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6222-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6222-188">b.</span><span class="sxs-lookup"><span data-stu-id="b6222-188">b.</span></span> <span data-ttu-id="b6222-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6222-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6222-190">c.</span><span class="sxs-lookup"><span data-stu-id="b6222-190">c.</span></span> <span data-ttu-id="b6222-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b6222-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6222-192">d.</span><span class="sxs-lookup"><span data-stu-id="b6222-192">d.</span></span> <span data-ttu-id="b6222-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b6222-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="b6222-194">Создание тестового пользователя Peoplecart</span><span class="sxs-lookup"><span data-stu-id="b6222-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="b6222-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="b6222-196">Обратитесь в [службу поддержки Peoplecart](https://peoplecart.com/ContactUs.aspx), чтобы добавить пользователей для платформы Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="b6222-197">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="b6222-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b6222-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6222-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="b6222-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="b6222-201">**Чтобы назначить пользователя Britta Simon в Peoplecart, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b6222-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="b6222-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6222-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b6222-204">В списке приложений выберите **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="b6222-204">In the applications list, select **Peoplecart**.</span></span>

    ![Ссылка на Peoplecart в списке "Приложения"](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="b6222-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6222-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="b6222-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6222-208">Click **Add** button.</span></span> <span data-ttu-id="b6222-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6222-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="b6222-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b6222-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6222-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b6222-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6222-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b6222-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b6222-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b6222-214">Test single sign-on</span></span>

<span data-ttu-id="b6222-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b6222-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b6222-216">Когда вы нажмете плитку Peoplecart на панели доступа, должна появиться страница входа в приложение Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="b6222-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="b6222-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6222-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6222-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6222-218">Additional resources</span></span>

* [<span data-ttu-id="b6222-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6222-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6222-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6222-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

