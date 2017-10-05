---
title: "Руководство по интеграции Azure Active Directory с Evernote | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="86696-103">Руководство по интеграции Azure Active Directory с Evernote</span><span class="sxs-lookup"><span data-stu-id="86696-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="86696-104">В этом руководстве описано, как интегрировать Evernote с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86696-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86696-105">Интеграция Evernote с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="86696-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86696-106">С помощью Azure AD вы можете контролировать доступ к Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="86696-107">Вы можете включить автоматический вход пользователей в Evernote (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86696-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="86696-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="86696-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="86696-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86696-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86696-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="86696-110">Prerequisites</span></span>

<span data-ttu-id="86696-111">Чтобы настроить интеграцию Azure AD с Evernote, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="86696-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="86696-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="86696-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86696-113">подписка с поддержкой единого входа Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86696-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="86696-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86696-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="86696-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86696-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="86696-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86696-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86696-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86696-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="86696-118">Scenario description</span></span>
<span data-ttu-id="86696-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="86696-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86696-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="86696-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86696-121">Добавление Evernote из коллекции.</span><span class="sxs-lookup"><span data-stu-id="86696-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="86696-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86696-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="86696-123">Добавление Evernote из коллекции</span><span class="sxs-lookup"><span data-stu-id="86696-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="86696-124">Чтобы настроить интеграцию Evernote с Azure AD, необходимо добавить Evernote из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="86696-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86696-125">**Чтобы добавить Evernote из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="86696-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86696-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86696-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="86696-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="86696-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86696-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86696-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="86696-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="86696-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="86696-133">В поле поиска введите **Evernote**, выберите **Evernote** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="86696-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote в списке результатов](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86696-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="86696-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="86696-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Evernote с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86696-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86696-137">Для настройки единого входа в Azure AD необходимо знать, какой пользователь в Evernote соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86696-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="86696-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="86696-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86696-140">Чтобы настроить и проверить единый вход Azure AD в Evernote, необходимо выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="86696-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86696-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="86696-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86696-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86696-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86696-143">**[Создание тестового пользователя Evernote](#create-an-evernote-test-user)** требуется для создания в Evernote пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86696-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86696-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86696-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86696-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="86696-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86696-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="86696-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86696-147">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="86696-148">**Чтобы настроить единый вход Azure AD в Evernote, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="86696-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="86696-149">На портале Azure на странице интеграции с приложением **Evernote** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="86696-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="86696-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="86696-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="86696-153">Если вы хотите настроить приложение в режиме, инициированном поставщиком удостоверений, в разделе **Домены и URL-адреса приложения Evernote** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="86696-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="86696-155">В текстовом поле **Идентификатор** введите URL-адрес `https://www.evernote.com/saml2`.</span><span class="sxs-lookup"><span data-stu-id="86696-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="86696-156">Установите флажок **Показать дополнительные параметры URL-адресов**, и выполните следующее действие, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="86696-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="86696-158">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="86696-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="86696-159">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="86696-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="86696-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="86696-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="86696-163">В разделе **Настройка Evernote** щелкните **Настроить Evernote**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="86696-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="86696-164">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="86696-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="86696-166">В другом окне веб-браузера войдите на сайт компании Evernote в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="86696-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="86696-167">Перейдите в **консоль администрирования**.</span><span class="sxs-lookup"><span data-stu-id="86696-167">Go to **'Admin Console'**</span></span>

    ![Консоль администрирования](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="86696-169">Из **консоли администрирования** перейдите в раздел **Безопасность** и выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="86696-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="86696-171">Задайте следующие значения.</span><span class="sxs-lookup"><span data-stu-id="86696-171">Configure the following values:</span></span>

    ![Настройка сертификата](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="86696-173">а.</span><span class="sxs-lookup"><span data-stu-id="86696-173">a.</span></span>  <span data-ttu-id="86696-174">**Включить единый вход**. Единый вход включен по умолчанию (щелкните **Отключить единый вход**, чтобы удалить требование единого входа).</span><span class="sxs-lookup"><span data-stu-id="86696-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="86696-175">b.</span><span class="sxs-lookup"><span data-stu-id="86696-175">b.</span></span> <span data-ttu-id="86696-176">Вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure, в текстовое поле **SAML HTTP Request URL** (URL-адрес HTTP-запроса SAML).</span><span class="sxs-lookup"><span data-stu-id="86696-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="86696-177">c.</span><span class="sxs-lookup"><span data-stu-id="86696-177">c.</span></span> <span data-ttu-id="86696-178">Откройте в Блокноте скачанный из Azure AD сертификат и скопируйте его содержимое, включая строки BEGIN CERTIFICATE и END CERTIFICATE, в текстовое поле **X.509 Certificate** (Сертификат X.509).</span><span class="sxs-lookup"><span data-stu-id="86696-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="86696-179">Щелкните **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="86696-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="86696-180">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="86696-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86696-181">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="86696-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86696-182">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="86696-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86696-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="86696-183">Create an Azure AD test user</span></span>

<span data-ttu-id="86696-184">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86696-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="86696-186">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="86696-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86696-187">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86696-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="86696-189">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="86696-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="86696-191">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="86696-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="86696-193">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="86696-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="86696-195">а.</span><span class="sxs-lookup"><span data-stu-id="86696-195">a.</span></span> <span data-ttu-id="86696-196">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86696-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86696-197">b.</span><span class="sxs-lookup"><span data-stu-id="86696-197">b.</span></span> <span data-ttu-id="86696-198">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86696-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="86696-199">c.</span><span class="sxs-lookup"><span data-stu-id="86696-199">c.</span></span> <span data-ttu-id="86696-200">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="86696-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="86696-201">г)</span><span class="sxs-lookup"><span data-stu-id="86696-201">d.</span></span> <span data-ttu-id="86696-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="86696-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="86696-203">Создание тестового пользователя Evernote</span><span class="sxs-lookup"><span data-stu-id="86696-203">Create an Evernote test user</span></span>

<span data-ttu-id="86696-204">Чтобы пользователи Azure AD могли выполнять вход в Evernote, они должны быть подготовлены для Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="86696-205">В случае с Evernote подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="86696-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="86696-206">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="86696-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="86696-207">Войдите на сайт компании Evernote в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="86696-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="86696-208">Щелкните **Консоль администрирования**.</span><span class="sxs-lookup"><span data-stu-id="86696-208">Click the **'Admin Console'**.</span></span>

    ![Консоль администрирования](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="86696-210">В **консоли администрирования** выберите **Добавить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="86696-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Добавление тестового пользователя](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="86696-212">**Добавьте адреса электронной почты участников команды** в **соответствующих полях** и нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="86696-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Добавление тестового пользователя](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="86696-214">После этого владелец учетной записи Azure Active Directory получает сообщение электронной почты, чтобы принять приглашение.</span><span class="sxs-lookup"><span data-stu-id="86696-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="86696-215">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="86696-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="86696-216">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход в Azure путем предоставления этому пользователю доступа к Evernote.</span><span class="sxs-lookup"><span data-stu-id="86696-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="86696-218">**Чтобы назначить пользователя Britta Simon в приложении Evernote, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="86696-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="86696-219">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="86696-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="86696-221">В списке приложений выберите **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="86696-221">In the applications list, select **Evernote**.</span></span>

    ![Ссылка на Evernote в списке "Приложения"](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="86696-223">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="86696-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="86696-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="86696-225">Click **Add** button.</span></span> <span data-ttu-id="86696-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="86696-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="86696-228">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="86696-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86696-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="86696-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86696-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="86696-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86696-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="86696-231">Test single sign-on</span></span>

<span data-ttu-id="86696-232">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="86696-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86696-233">Щелкнув плитку Evernote на панели доступа, вы автоматически войдете в приложение.</span><span class="sxs-lookup"><span data-stu-id="86696-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="86696-234">Будет выполнен вход с использованием учетной записи организации, но затем нужно будет войти с помощью личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="86696-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="86696-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="86696-235">Additional resources</span></span>

* [<span data-ttu-id="86696-236">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86696-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86696-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86696-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

