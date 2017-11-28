---
title: "Руководство по интеграции Azure Active Directory с PagerDuty | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="9a830-103">Руководство по интеграции Azure Active Directory с PagerDuty</span><span class="sxs-lookup"><span data-stu-id="9a830-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="9a830-104">В этом руководстве описано, как интегрировать PagerDuty с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a830-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a830-105">Интеграция Azure AD с приложением PagerDuty обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="9a830-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a830-106">С помощью Azure AD вы можете контролировать доступ к PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="9a830-107">Вы можете включить автоматический вход пользователей в PagerDuty (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a830-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a830-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9a830-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a830-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a830-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a830-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a830-110">Prerequisites</span></span>

<span data-ttu-id="9a830-111">Чтобы настроить интеграцию Azure AD с приложением PagerDuty, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9a830-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="9a830-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9a830-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a830-113">подписка PagerDuty с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a830-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a830-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9a830-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a830-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9a830-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a830-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9a830-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a830-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a830-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a830-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9a830-118">Scenario description</span></span>
<span data-ttu-id="9a830-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9a830-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a830-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9a830-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a830-121">Добавление PagerDuty из коллекции</span><span class="sxs-lookup"><span data-stu-id="9a830-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="9a830-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a830-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="9a830-123">Добавление PagerDuty из коллекции</span><span class="sxs-lookup"><span data-stu-id="9a830-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="9a830-124">Чтобы настроить интеграцию PagerDuty с Azure AD, необходимо добавить PagerDuty из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a830-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a830-125">**Чтобы добавить PagerDuty из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a830-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a830-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a830-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="9a830-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a830-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a830-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a830-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="9a830-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9a830-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="9a830-133">В поле поиска введите **PagerDuty**, выберите **PagerDuty** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="9a830-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a830-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a830-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a830-136">В этом разделе описана настройка и проверка единого входа Azure AD в PagerDuty с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a830-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a830-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в PagerDuty соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a830-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="9a830-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="9a830-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a830-140">Чтобы настроить и проверить единый вход Azure AD в PagerDuty, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="9a830-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a830-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9a830-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a830-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a830-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a830-143">**[Создание тестового пользователя PagerDuty](#create-a-pagerduty-test-user)** требуется для того, чтобы в PagerDuty существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a830-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a830-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a830-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a830-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9a830-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a830-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a830-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a830-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="9a830-148">**Чтобы настроить единый вход Azure AD в PagerDuty, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a830-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="9a830-149">На портале Azure на странице интеграции с приложением **PagerDuty** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9a830-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="9a830-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a830-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="9a830-153">В разделе **Домены и URL-адреса приложения PagerDuty** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a830-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="9a830-155">а.</span><span class="sxs-lookup"><span data-stu-id="9a830-155">a.</span></span> <span data-ttu-id="9a830-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="9a830-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="9a830-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a830-157">b.</span></span> <span data-ttu-id="9a830-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="9a830-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a830-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9a830-159">These values are not real.</span></span> <span data-ttu-id="9a830-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="9a830-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9a830-161">Чтобы получить их, обратитесь в [службу поддержки клиентов PagerDuty](https://www.pagerduty.com/support/).</span><span class="sxs-lookup"><span data-stu-id="9a830-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="9a830-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a830-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="9a830-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9a830-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a830-166">В разделе **Конфигурация PagerDuty** щелкните **Настроить PagerDuty**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9a830-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9a830-167">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9a830-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="9a830-169">В другом окне браузера войдите на свой сайт PagerDuty компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9a830-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="9a830-170">В меню в верхней части страницы щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="9a830-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="9a830-171">![Параметры учетной записи](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="9a830-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="9a830-172">Щелкните **Single Sign-on**(Единый вход).</span><span class="sxs-lookup"><span data-stu-id="9a830-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="9a830-173">![Единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="9a830-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="9a830-174">На странице **Включить единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a830-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="9a830-175">![Разрешить единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Разрешить единый вход")</span><span class="sxs-lookup"><span data-stu-id="9a830-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="9a830-176">а.</span><span class="sxs-lookup"><span data-stu-id="9a830-176">a.</span></span> <span data-ttu-id="9a830-177">Откройте в Блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **X.509 Certificate** (Сертификат X.509).</span><span class="sxs-lookup"><span data-stu-id="9a830-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="9a830-178">b.</span><span class="sxs-lookup"><span data-stu-id="9a830-178">b.</span></span> <span data-ttu-id="9a830-179">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9a830-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="9a830-180">c.</span><span class="sxs-lookup"><span data-stu-id="9a830-180">c.</span></span> <span data-ttu-id="9a830-181">В текстовое поле **Logout URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9a830-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="9a830-182">d.</span><span class="sxs-lookup"><span data-stu-id="9a830-182">d.</span></span> <span data-ttu-id="9a830-183">Установите флажок **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9a830-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="9a830-184">д.</span><span class="sxs-lookup"><span data-stu-id="9a830-184">e.</span></span> <span data-ttu-id="9a830-185">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="9a830-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="9a830-186">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9a830-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a830-187">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9a830-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a830-188">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9a830-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a830-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a830-189">Create an Azure AD test user</span></span>

<span data-ttu-id="9a830-190">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a830-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="9a830-192">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9a830-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a830-193">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a830-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a830-195">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9a830-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a830-197">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a830-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a830-199">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a830-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a830-201">а.</span><span class="sxs-lookup"><span data-stu-id="9a830-201">a.</span></span> <span data-ttu-id="9a830-202">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a830-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a830-203">b.</span><span class="sxs-lookup"><span data-stu-id="9a830-203">b.</span></span> <span data-ttu-id="9a830-204">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a830-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a830-205">c.</span><span class="sxs-lookup"><span data-stu-id="9a830-205">c.</span></span> <span data-ttu-id="9a830-206">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9a830-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a830-207">d.</span><span class="sxs-lookup"><span data-stu-id="9a830-207">d.</span></span> <span data-ttu-id="9a830-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a830-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="9a830-209">Создание тестового пользователя PagerDuty</span><span class="sxs-lookup"><span data-stu-id="9a830-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="9a830-210">Чтобы пользователи Azure AD могли выполнять вход в PagerDuty, они должны быть подготовлены для PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="9a830-211">В случае с PagerDuty подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9a830-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="9a830-212">Вы можете использовать любые другие инструменты создания учетных записей пользователя PagerDuty или API, предоставляемые PagerDuty для подготовки учетных записей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a830-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="9a830-213">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="9a830-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9a830-214">Выполните вход в клиент **PagerDuty** .</span><span class="sxs-lookup"><span data-stu-id="9a830-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="9a830-215">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9a830-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="9a830-216">Щелкните **Добавить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9a830-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="9a830-217">![Добавление пользователей](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="9a830-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="9a830-218">В диалоговом окне **Invite your team** (Пригласить команду) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a830-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="9a830-219">![Пригласить команду](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Пригласить команду")</span><span class="sxs-lookup"><span data-stu-id="9a830-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="9a830-220">а.</span><span class="sxs-lookup"><span data-stu-id="9a830-220">a.</span></span> <span data-ttu-id="9a830-221">В текстовое поле **First and Last Name** (Имя и фамилия) введите сведения о пользователе, например **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a830-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="9a830-222">b.</span><span class="sxs-lookup"><span data-stu-id="9a830-222">b.</span></span> <span data-ttu-id="9a830-223">Введите **Email** (Адрес электронной почты) для пользователя, например: **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9a830-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="9a830-224">c.</span><span class="sxs-lookup"><span data-stu-id="9a830-224">c.</span></span> <span data-ttu-id="9a830-225">Нажмите **Add** (Добавить), затем нажмите **Send Invites** (Отправить приглашения).</span><span class="sxs-lookup"><span data-stu-id="9a830-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9a830-226">Все добавленные пользователи получат приглашение создать учетную запись PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9a830-227">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a830-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="9a830-228">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Назначение роли пользователя][200]

<span data-ttu-id="9a830-230">**Чтобы назначить пользователя Britta Simon в PagerDuty, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a830-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="9a830-231">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a830-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9a830-233">В списке приложений выберите **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="9a830-233">In the applications list, select **PagerDuty**.</span></span>

    ![Ссылка на PagerDuty в списке "Приложения"](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="9a830-235">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a830-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="9a830-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a830-237">Click **Add** button.</span></span> <span data-ttu-id="9a830-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a830-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="9a830-240">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a830-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a830-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9a830-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a830-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9a830-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a830-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9a830-243">Test single sign-on</span></span>

<span data-ttu-id="9a830-244">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9a830-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a830-245">Щелкнув элемент PagerDuty на панели доступа, вы автоматически войдете в приложение PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="9a830-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="9a830-246">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a830-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a830-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9a830-247">Additional resources</span></span>

* [<span data-ttu-id="9a830-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a830-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a830-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a830-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

