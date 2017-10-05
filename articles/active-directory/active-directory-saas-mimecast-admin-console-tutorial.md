---
title: "Учебник. Интеграция Azure Active Directory с консолью администрирования Mimecast | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в консоль администрирования Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="bbc92-103">Учебник. Интеграция Azure Active Directory с консолью администрирования Mimecast</span><span class="sxs-lookup"><span data-stu-id="bbc92-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="bbc92-104">В этом руководстве описано, как интегрировать консоль администрирования Mimecast с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbc92-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbc92-105">Интеграция Azure AD с консолью администрирования Mimecast обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bbc92-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbc92-106">С помощью Azure AD вы можете контролировать доступ к консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="bbc92-107">Вы можете включить автоматический вход пользователей в консоль администрирования Mimecast (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc92-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bbc92-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc92-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bbc92-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbc92-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbc92-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bbc92-110">Prerequisites</span></span>

<span data-ttu-id="bbc92-111">Чтобы настроить интеграцию Azure AD с консолью администрирования Mimecast, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bbc92-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="bbc92-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bbc92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbc92-113">Подписка на консоль администрирования Mimecast с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="bbc92-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbc92-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bbc92-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbc92-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="bbc92-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbc92-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bbc92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbc92-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbc92-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbc92-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bbc92-118">Scenario description</span></span>
<span data-ttu-id="bbc92-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bbc92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbc92-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="bbc92-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbc92-121">Добавление консоли администрирования Mimecast из коллекции</span><span class="sxs-lookup"><span data-stu-id="bbc92-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="bbc92-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="bbc92-123">Добавление консоли администрирования Mimecast из коллекции</span><span class="sxs-lookup"><span data-stu-id="bbc92-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="bbc92-124">Чтобы настроить интеграцию консоли администрирования Mimecast с Azure AD, необходимо добавить консоль администрирования Mimecast из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bbc92-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbc92-125">**Чтобы добавить консоль администрирования Mimecast из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="bbc92-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc92-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="bbc92-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbc92-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="bbc92-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="bbc92-133">В поле поиска введите **Консоль администрирования Mimecast**, выберите **Консоль администрирования Mimecast** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="bbc92-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Консоль администрирования Mimecast в списке результатов](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbc92-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc92-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bbc92-136">В этом разделе описана настройка и проверка единого входа Azure AD в консоли администрирования Mimecast с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc92-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbc92-137">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в консоли администрирования Mimecast соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc92-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="bbc92-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="bbc92-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbc92-140">Чтобы настроить и проверить единый вход Azure AD в консоли администрирования Mimecast, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="bbc92-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbc92-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="bbc92-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbc92-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc92-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbc92-143">**[Создание тестового пользователя консоли администрирования Mimecast](#create-a-mimecast-admin-console-test-user)** требуется для того, чтобы в консоли администрирования Mimecast существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc92-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbc92-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc92-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbc92-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bbc92-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bbc92-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc92-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bbc92-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="bbc92-148">**Чтобы настроить единый вход Azure AD в консоли администрирования Mimecast, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="bbc92-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc92-149">На портале Azure на странице интеграции с приложением **Консоль администрирования Mimecast** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="bbc92-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="bbc92-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="bbc92-153">В разделе **Домены и URL-адреса консоли администрирования Mimecast** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bbc92-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа консоли администрирования Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="bbc92-155">В текстовом поле **URL-адрес для входа** введите URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="bbc92-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="bbc92-156">URL-адрес для входа зависит от региона.</span><span class="sxs-lookup"><span data-stu-id="bbc92-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="bbc92-157">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bbc92-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="bbc92-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bbc92-159">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbc92-161">В разделе **Конфигурация консоли администрирования Mimecast** щелкните **Настроить консоль администрирования Mimecast**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbc92-162">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка консоли администрирования Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="bbc92-164">В другом окне веб-браузера войдите в консоль администрирования Mimecast в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bbc92-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="bbc92-165">Выберите **Services \> Application** (Службы > Приложение).</span><span class="sxs-lookup"><span data-stu-id="bbc92-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="bbc92-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services") (Службы)</span><span class="sxs-lookup"><span data-stu-id="bbc92-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="bbc92-167">Щелкните **Профили проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="bbc92-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles") (Профили аутентификации)</span><span class="sxs-lookup"><span data-stu-id="bbc92-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="bbc92-169">Щелкните **Новый профиль проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="bbc92-170">![New Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profile") (Создать профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="bbc92-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="bbc92-171">В разделе **Профиль проверки подлинности** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bbc92-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="bbc92-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile") (Профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="bbc92-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="bbc92-173">а.</span><span class="sxs-lookup"><span data-stu-id="bbc92-173">a.</span></span> <span data-ttu-id="bbc92-174">В текстовом поле **Описание** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bbc92-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="bbc92-175">b.</span><span class="sxs-lookup"><span data-stu-id="bbc92-175">b.</span></span> <span data-ttu-id="bbc92-176">Выберите **Обязательное использование проверки подлинности SAML для консоли администрирования Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="bbc92-177">c.</span><span class="sxs-lookup"><span data-stu-id="bbc92-177">c.</span></span> <span data-ttu-id="bbc92-178">В поле **Provider** (Поставщик) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="bbc92-179">d.</span><span class="sxs-lookup"><span data-stu-id="bbc92-179">d.</span></span> <span data-ttu-id="bbc92-180">Вставьте **идентификатор сущности SAML**, скопированный на портале Azure, в текстовое поле **URL-адрес издателя**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="bbc92-181">д.</span><span class="sxs-lookup"><span data-stu-id="bbc92-181">e.</span></span> <span data-ttu-id="bbc92-182">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc92-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="bbc92-183">f.</span><span class="sxs-lookup"><span data-stu-id="bbc92-183">f.</span></span> <span data-ttu-id="bbc92-184">В текстовое поле **Logout URL** (URL-адрес выхода) вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc92-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="bbc92-185">Значения URL-адреса входа в систему и URL-адреса выхода из системы для консоли администрирования Mimecast одинаковы.</span><span class="sxs-lookup"><span data-stu-id="bbc92-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="bbc92-186">ж.</span><span class="sxs-lookup"><span data-stu-id="bbc92-186">g.</span></span> <span data-ttu-id="bbc92-187">Откройте в Блокноте скачанный на портале Azure сертификат в кодировке Base-64, удалите первую строку ("*--*") и последнюю строку ("*--*"), скопируйте остальное содержимое в буфер обмена и вставьте его в текстовое поле **Identity Provider Certificate (Metadata)** (Сертификат поставщика удостоверений (метаданные)).</span><span class="sxs-lookup"><span data-stu-id="bbc92-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="bbc92-188">h.</span><span class="sxs-lookup"><span data-stu-id="bbc92-188">h.</span></span> <span data-ttu-id="bbc92-189">Установите флажок **Разрешить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="bbc92-190">i.</span><span class="sxs-lookup"><span data-stu-id="bbc92-190">i.</span></span> <span data-ttu-id="bbc92-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bbc92-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="bbc92-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbc92-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bbc92-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbc92-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="bbc92-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbc92-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc92-195">Create an Azure AD test user</span></span>

<span data-ttu-id="bbc92-196">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc92-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="bbc92-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bbc92-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc92-199">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bbc92-201">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bbc92-203">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bbc92-205">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="bbc92-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bbc92-207">а.</span><span class="sxs-lookup"><span data-stu-id="bbc92-207">a.</span></span> <span data-ttu-id="bbc92-208">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbc92-209">b.</span><span class="sxs-lookup"><span data-stu-id="bbc92-209">b.</span></span> <span data-ttu-id="bbc92-210">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc92-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bbc92-211">c.</span><span class="sxs-lookup"><span data-stu-id="bbc92-211">c.</span></span> <span data-ttu-id="bbc92-212">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bbc92-213">г)</span><span class="sxs-lookup"><span data-stu-id="bbc92-213">d.</span></span> <span data-ttu-id="bbc92-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="bbc92-215">Создание тестового пользователя консоли администрирования Mimecast</span><span class="sxs-lookup"><span data-stu-id="bbc92-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="bbc92-216">Чтобы разрешить пользователям Azure AD вход в консоль администрирования Mimecast, они должны быть подготовлены для консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="bbc92-217">В случае с консолью администрирования Mimecast подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="bbc92-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="bbc92-218">Перед созданием пользователей необходимо зарегистрировать домен.</span><span class="sxs-lookup"><span data-stu-id="bbc92-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="bbc92-219">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="bbc92-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc92-220">Войдите в **консоль администрирования Mimecast** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bbc92-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="bbc92-221">Выберите **Directories \> Internal** (Каталоги > Внутренние).</span><span class="sxs-lookup"><span data-stu-id="bbc92-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="bbc92-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories") (Каталоги)</span><span class="sxs-lookup"><span data-stu-id="bbc92-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="bbc92-223">Щелкните **Зарегистрировать новый домен**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="bbc92-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain") (Зарегистрировать новый домен)</span><span class="sxs-lookup"><span data-stu-id="bbc92-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="bbc92-225">После создания нового домена щелкните **Новый адрес**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="bbc92-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address") (Новый адрес)</span><span class="sxs-lookup"><span data-stu-id="bbc92-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="bbc92-227">В окне нового адреса выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bbc92-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="bbc92-228">![Сохранить](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="bbc92-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="bbc92-229">а.</span><span class="sxs-lookup"><span data-stu-id="bbc92-229">a.</span></span> <span data-ttu-id="bbc92-230">В соответствующие текстовые поля введите атрибуты **Email Address** (Адрес электронной почты), **Global Name** (Глобальное имя), **Password** (Пароль) и **Confirm Password** (Подтверждение пароля) действительной учетной записи Azure AD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="bbc92-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="bbc92-231">b.</span><span class="sxs-lookup"><span data-stu-id="bbc92-231">b.</span></span> <span data-ttu-id="bbc92-232">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="bbc92-233">Вы можете использовать любые другие средства создания учетных записей консоли администрирования Mimecast или API, предоставляемые консолью администрирования Mimecast для подготовки учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc92-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bbc92-234">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc92-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="bbc92-235">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="bbc92-237">**Чтобы назначить пользователя Britta Simon в консоли администрирования Mimecast, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="bbc92-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc92-238">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bbc92-240">Из списка приложений выберите **Консоль администрирования Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![Ссылка на консоль администрирования Mimecast в списке "Приложения"](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="bbc92-242">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="bbc92-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-244">Click **Add** button.</span></span> <span data-ttu-id="bbc92-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="bbc92-247">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbc92-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbc92-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bbc92-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbc92-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bbc92-250">Test single sign-on</span></span>

<span data-ttu-id="bbc92-251">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="bbc92-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bbc92-252">Щелкнув элемент "Консоль администрирования Mimecast" на панели доступа, вы автоматически войдете в приложение консоли администрирования Mimecast.</span><span class="sxs-lookup"><span data-stu-id="bbc92-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="bbc92-253">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbc92-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bbc92-254">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bbc92-254">Additional resources</span></span>

* [<span data-ttu-id="bbc92-255">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbc92-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbc92-256">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbc92-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

