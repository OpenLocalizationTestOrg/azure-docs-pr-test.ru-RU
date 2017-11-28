---
title: "Учебник. Интеграция Azure Active Directory с ICIMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="64f99-103">Руководство. Интеграция Azure Active Directory с ICIMS</span><span class="sxs-lookup"><span data-stu-id="64f99-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="64f99-104">В этом руководстве описано, как интегрировать ICIMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64f99-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64f99-105">Интеграция Azure AD с приложением ICIMS обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="64f99-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="64f99-106">С помощью Azure AD вы можете контролировать доступ к ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="64f99-107">Вы можете включить автоматический вход пользователей в ICIMS (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64f99-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64f99-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="64f99-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="64f99-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="64f99-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64f99-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="64f99-110">Prerequisites</span></span>

<span data-ttu-id="64f99-111">Чтобы настроить интеграцию Azure AD с ICIMS, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="64f99-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="64f99-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="64f99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64f99-113">подписка ICIMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="64f99-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64f99-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="64f99-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64f99-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="64f99-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64f99-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="64f99-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="64f99-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64f99-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64f99-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="64f99-118">Scenario description</span></span>
<span data-ttu-id="64f99-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="64f99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64f99-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="64f99-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64f99-121">Добавление ICIMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="64f99-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="64f99-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64f99-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="64f99-123">Добавление ICIMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="64f99-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="64f99-124">Чтобы настроить интеграцию ICIMS с Azure AD, необходимо добавить ICIMS из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="64f99-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="64f99-125">**Чтобы добавить ICIMS из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="64f99-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="64f99-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64f99-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="64f99-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="64f99-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="64f99-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="64f99-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="64f99-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="64f99-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="64f99-133">В поле поиска введите **ICIMS**, выберите **ICIMS** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="64f99-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS в списке результатов](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="64f99-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f99-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="64f99-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ICIMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64f99-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64f99-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ICIMS соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64f99-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="64f99-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="64f99-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="64f99-140">Чтобы настроить и проверить единый вход Azure AD в ICIMS, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="64f99-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="64f99-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="64f99-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="64f99-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64f99-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64f99-143">**[Создание тестового пользователя ICIMS](#create-an-icims-test-user)** требуется для создания в ICIMS пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64f99-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="64f99-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64f99-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64f99-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="64f99-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="64f99-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f99-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="64f99-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="64f99-148">**Чтобы настроить единый вход Azure AD в ICIMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="64f99-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="64f99-149">На портале Azure на странице интеграции с приложением **ICIMS** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="64f99-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="64f99-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="64f99-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="64f99-153">В разделе **Домены и URL-адреса приложения ICIMS** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="64f99-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="64f99-155">а.</span><span class="sxs-lookup"><span data-stu-id="64f99-155">a.</span></span> <span data-ttu-id="64f99-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="64f99-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="64f99-157">b.</span><span class="sxs-lookup"><span data-stu-id="64f99-157">b.</span></span> <span data-ttu-id="64f99-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="64f99-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64f99-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="64f99-159">These values are not real.</span></span> <span data-ttu-id="64f99-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="64f99-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="64f99-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="64f99-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="64f99-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="64f99-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="64f99-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="64f99-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="64f99-166">В разделе **Конфигурация ICIMS** щелкните **Настроить ICIMS**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="64f99-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="64f99-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="64f99-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="64f99-169">Чтобы настроить единый вход на стороне **ICIMS**, нужно передать скачанный **XML-файл метаданных**, а также **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="64f99-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="64f99-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="64f99-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="64f99-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="64f99-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="64f99-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="64f99-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="64f99-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="64f99-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="64f99-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f99-174">Create an Azure AD test user</span></span>
<span data-ttu-id="64f99-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="64f99-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="64f99-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="64f99-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="64f99-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64f99-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64f99-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="64f99-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64f99-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="64f99-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64f99-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="64f99-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64f99-186">а.</span><span class="sxs-lookup"><span data-stu-id="64f99-186">a.</span></span> <span data-ttu-id="64f99-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="64f99-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64f99-188">b.</span><span class="sxs-lookup"><span data-stu-id="64f99-188">b.</span></span> <span data-ttu-id="64f99-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="64f99-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64f99-190">c.</span><span class="sxs-lookup"><span data-stu-id="64f99-190">c.</span></span> <span data-ttu-id="64f99-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="64f99-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="64f99-192">d.</span><span class="sxs-lookup"><span data-stu-id="64f99-192">d.</span></span> <span data-ttu-id="64f99-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="64f99-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="64f99-194">Создание тестового пользователя ICIMS</span><span class="sxs-lookup"><span data-stu-id="64f99-194">Create an ICIMS test user</span></span>

<span data-ttu-id="64f99-195">Цель этого раздела — создать пользователя с именем Britta Simon в приложении ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="64f99-196">Обратитесь в [службу поддержки ICIMS](https://www.icims.com/contact-us), чтобы добавить пользователей в учетную запись ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="64f99-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f99-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="64f99-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Назначение роли пользователя][200]

<span data-ttu-id="64f99-200">**Чтобы назначить пользователя Britta Simon в ICIMS, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="64f99-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="64f99-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="64f99-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="64f99-203">В списке приложений выберите **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="64f99-203">In the applications list, select **ICIMS**.</span></span>

    ![Ссылка на ICIMS в списке "Приложения"](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="64f99-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="64f99-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="64f99-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="64f99-207">Click **Add** button.</span></span> <span data-ttu-id="64f99-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="64f99-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="64f99-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="64f99-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="64f99-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="64f99-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64f99-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="64f99-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="64f99-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="64f99-213">Test single sign-on</span></span>

<span data-ttu-id="64f99-214">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="64f99-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="64f99-215">Щелкнув элемент ICIMS на панели доступа, вы автоматически войдете в приложение ICIMS.</span><span class="sxs-lookup"><span data-stu-id="64f99-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64f99-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="64f99-216">Additional resources</span></span>

* [<span data-ttu-id="64f99-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64f99-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64f99-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="64f99-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

