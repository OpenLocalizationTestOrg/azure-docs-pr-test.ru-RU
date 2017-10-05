---
title: "Руководство по интеграции Azure Active Directory с Yonyx Interactive Guides | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Yonyx Interactive Guides."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 522f440a0b3746e1101aed845678b3930e030fec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="7de63-103">Руководство по интеграции Azure Active Directory с Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="7de63-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="7de63-104">В этом руководстве описано, как интегрировать Yonyx Interactive Guides с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7de63-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7de63-105">Интеграция Azure AD с приложением Yonyx Interactive Guides обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7de63-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7de63-106">С помощью Azure AD вы можете контролировать доступ к Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
- <span data-ttu-id="7de63-107">Вы можете включить автоматический вход пользователей в Yonyx Interactive Guides (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de63-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7de63-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7de63-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7de63-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7de63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7de63-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7de63-110">Prerequisites</span></span>

<span data-ttu-id="7de63-111">Чтобы настроить интеграцию Azure AD с Yonyx Interactive Guides, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7de63-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

- <span data-ttu-id="7de63-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7de63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7de63-113">подписка Yonyx Interactive Guides с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7de63-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7de63-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7de63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7de63-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7de63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7de63-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7de63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7de63-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7de63-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7de63-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7de63-118">Scenario description</span></span>
<span data-ttu-id="7de63-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7de63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7de63-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7de63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7de63-121">Добавление Yonyx Interactive Guides из коллекции</span><span class="sxs-lookup"><span data-stu-id="7de63-121">Adding Yonyx Interactive Guides from the gallery</span></span>
2. <span data-ttu-id="7de63-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="7de63-123">Добавление Yonyx Interactive Guides из коллекции</span><span class="sxs-lookup"><span data-stu-id="7de63-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="7de63-124">Чтобы настроить интеграцию Yonyx Interactive Guides с Azure AD, необходимо добавить Yonyx Interactive Guides из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7de63-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7de63-125">**Чтобы добавить Yonyx Interactive Guides из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7de63-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7de63-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7de63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="7de63-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de63-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7de63-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de63-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="7de63-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7de63-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="7de63-133">В поле поиска введите **Yonyx Interactive Guides**, выберите **Yonyx Interactive Guides** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="7de63-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span></span>

    ![Yonyx Interactive Guides в списке результатов](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7de63-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de63-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7de63-136">В этом разделе описана настройка и проверка единого входа Azure AD в Yonyx Interactive Guides с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de63-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7de63-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Yonyx Interactive Guides соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de63-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span></span> <span data-ttu-id="7de63-138">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="7de63-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7de63-140">Чтобы настроить и проверить единый вход Azure AD в Yonyx Interactive Guides, вам потребуется выполнить следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="7de63-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7de63-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7de63-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7de63-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de63-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7de63-143">**[Создание тестового пользователя Yonyx Interactive Guides](#create-a-yonyx-interactive-guides-test-user)**. Требуется для создания в Yonyx Interactive Guides пользователя Britta Simon, связанного с соответствующим представлением пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de63-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7de63-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de63-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7de63-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7de63-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7de63-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de63-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7de63-147">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="7de63-148">**Чтобы настроить единый вход Azure AD в Yonyx Interactive Guides, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7de63-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="7de63-149">На портале Azure на странице интеграции с приложением **Yonyx Interactive Guides** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7de63-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="7de63-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7de63-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="7de63-153">В разделе **Домены и URL-адреса приложения Yonyx Interactive Guides** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7de63-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="7de63-155">а.</span><span class="sxs-lookup"><span data-stu-id="7de63-155">a.</span></span> <span data-ttu-id="7de63-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="7de63-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="7de63-157">b.</span><span class="sxs-lookup"><span data-stu-id="7de63-157">b.</span></span> <span data-ttu-id="7de63-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="7de63-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7de63-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7de63-159">These values are not real.</span></span> <span data-ttu-id="7de63-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="7de63-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7de63-161">Чтобы получить эти значения, обратитесь в [службу поддержки Yonyx Interactive Guides](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="7de63-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span></span> 
 
4. <span data-ttu-id="7de63-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7de63-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="7de63-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7de63-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7de63-166">В разделе **Конфигурация Yonyx Interactive Guides** нажмите **Настроить Yonyx Interactive Guides**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7de63-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7de63-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="7de63-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="7de63-169">Чтобы настроить единый вход на стороне **Yonyx Interactive Guides**, нужно отправить скачанный **сертификат в кодировке Base64**, **URL-адрес выхода**, **URL-адрес службы единого входа SAML** и **идентификатор сущности SAML** [группе поддержки Yonyx Interactive Guides](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="7de63-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="7de63-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="7de63-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7de63-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7de63-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7de63-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7de63-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7de63-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7de63-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7de63-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de63-174">Create an Azure AD test user</span></span>

<span data-ttu-id="7de63-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de63-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

  ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="7de63-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7de63-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7de63-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7de63-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7de63-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7de63-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7de63-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7de63-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7de63-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7de63-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7de63-186">а.</span><span class="sxs-lookup"><span data-stu-id="7de63-186">a.</span></span> <span data-ttu-id="7de63-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7de63-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7de63-188">b.</span><span class="sxs-lookup"><span data-stu-id="7de63-188">b.</span></span> <span data-ttu-id="7de63-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7de63-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7de63-190">c.</span><span class="sxs-lookup"><span data-stu-id="7de63-190">c.</span></span> <span data-ttu-id="7de63-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7de63-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7de63-192">d.</span><span class="sxs-lookup"><span data-stu-id="7de63-192">d.</span></span> <span data-ttu-id="7de63-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7de63-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="7de63-194">Создание тестового пользователя Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="7de63-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="7de63-195">Цель этого раздела — создать в приложении Yonyx Interactive Guides пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de63-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="7de63-196">Приложение Yonyx Interactive Guides поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7de63-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7de63-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="7de63-197">There is no action item for you in this section.</span></span> <span data-ttu-id="7de63-198">При попытке получить доступ к Yonyx Interactive Guides создается пользователь (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="7de63-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7de63-199">Чтобы создать пользователя вручную, необходимо обратиться в службу поддержки Yonyx Interactive Guides по адресу <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="7de63-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7de63-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de63-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="7de63-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span></span>

![Назначение роли пользователя][200]

<span data-ttu-id="7de63-203">**Чтобы назначить пользователя Britta Simon в Yonyx Interactive Guides, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7de63-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="7de63-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de63-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7de63-206">В списке приложений выберите **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="7de63-206">In the applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Ссылка на Yonyx Interactive Guides в списке приложений](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="7de63-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7de63-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="7de63-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7de63-210">Click **Add** button.</span></span> <span data-ttu-id="7de63-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7de63-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="7de63-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7de63-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7de63-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7de63-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7de63-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7de63-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7de63-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7de63-216">Test single sign-on</span></span>

<span data-ttu-id="7de63-217">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7de63-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7de63-218">Щелкнув элемент Yonyx Interactive Guides на панели доступа, вы автоматически войдете в приложение Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="7de63-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="7de63-219">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7de63-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7de63-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7de63-220">Additional resources</span></span>

* [<span data-ttu-id="7de63-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7de63-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7de63-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7de63-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

