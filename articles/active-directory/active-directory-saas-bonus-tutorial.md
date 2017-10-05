---
title: "Руководство по интеграции Azure Active Directory с Bonusly | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="af0a9-103">Руководство. Интеграция Azure Active Directory с Bonusly</span><span class="sxs-lookup"><span data-stu-id="af0a9-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="af0a9-104">В этом руководстве описано, как интегрировать Bonusly с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af0a9-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af0a9-105">Интеграция Azure AD с приложением Bonusly обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="af0a9-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="af0a9-106">c помощью Azure AD вы можете контролировать доступ к приложению Bonusly;</span><span class="sxs-lookup"><span data-stu-id="af0a9-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="af0a9-107">вы можете включить автоматический вход пользователей в Bonusly (единый вход) с учетной записью Azure AD;</span><span class="sxs-lookup"><span data-stu-id="af0a9-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af0a9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="af0a9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af0a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af0a9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="af0a9-110">Prerequisites</span></span>

<span data-ttu-id="af0a9-111">Чтобы настроить интеграцию Azure AD с приложением Bonusly, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="af0a9-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="af0a9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="af0a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af0a9-113">подписка Bonusly с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="af0a9-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af0a9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="af0a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af0a9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="af0a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af0a9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="af0a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af0a9-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af0a9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af0a9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="af0a9-118">Scenario description</span></span>
<span data-ttu-id="af0a9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="af0a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af0a9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="af0a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af0a9-121">Добавление Bonusly из коллекции</span><span class="sxs-lookup"><span data-stu-id="af0a9-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="af0a9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="af0a9-123">Добавление Bonusly из коллекции</span><span class="sxs-lookup"><span data-stu-id="af0a9-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="af0a9-124">Чтобы настроить интеграцию Bonusly с Azure AD, необходимо добавить Bonusly из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="af0a9-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af0a9-125">**Чтобы добавить Bonusly из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="af0a9-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af0a9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="af0a9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="af0a9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="af0a9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="af0a9-133">В поле поиска введите **Bonusly**, выберите **Bonusly** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="af0a9-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![Bonusly в списке результатов](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="af0a9-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0a9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="af0a9-136">В этом разделе описана настройка и проверка единого входа Azure AD в Bonusly с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af0a9-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af0a9-137">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Bonusly соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0a9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="af0a9-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="af0a9-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="af0a9-140">Чтобы настроить и проверить единый вход Azure AD в Bonusly, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="af0a9-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af0a9-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="af0a9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af0a9-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af0a9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af0a9-143">**[Создание тестового пользователя Bonusly](#create-a-bonusly-test-user)** требуется для того, чтобы в Bonusly существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0a9-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="af0a9-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af0a9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af0a9-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="af0a9-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="af0a9-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0a9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="af0a9-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="af0a9-148">**Чтобы настроить единый вход Azure AD в Bonusly, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="af0a9-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="af0a9-149">На портале Azure на странице интеграции с приложением **Bonusly** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="af0a9-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="af0a9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="af0a9-153">В разделе **Домены и URL-адреса приложения Bonusly** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="af0a9-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах для единого входа в приложение Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="af0a9-155">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://Bonus.ly/saml/<tenant-name>`.</span><span class="sxs-lookup"><span data-stu-id="af0a9-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="af0a9-156">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="af0a9-156">The value is not real.</span></span> <span data-ttu-id="af0a9-157">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="af0a9-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="af0a9-158">Чтобы получить это значение, обратитесь в [службу поддержки Bonusly](https://Bonusly/contact).</span><span class="sxs-lookup"><span data-stu-id="af0a9-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="af0a9-159">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток** сертификата.</span><span class="sxs-lookup"><span data-stu-id="af0a9-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="af0a9-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="af0a9-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af0a9-163">В разделе **Настройка Bonusly** щелкните **Настроить Bonusly**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="af0a9-164">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="af0a9-166">В другом окне браузера войдите в клиент **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="af0a9-167">На панели инструментов в верхней части экрана щелкните **Settings** (Параметры) и выберите **Integrations and apps** (Интеграции и приложения).</span><span class="sxs-lookup"><span data-stu-id="af0a9-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="af0a9-168">![Социальный раздел Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="af0a9-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="af0a9-169">В разделе **Single Sign-On** (Единый вход) выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="af0a9-170">На диалоговой странице **SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="af0a9-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="af0a9-171">![Диалоговое окно SAML в Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="af0a9-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="af0a9-172">а.</span><span class="sxs-lookup"><span data-stu-id="af0a9-172">a.</span></span> <span data-ttu-id="af0a9-173">В текстовое поле **IdP SSO target URL** (Целевой URL-адрес единого входа IdP) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a9-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="af0a9-174">b.</span><span class="sxs-lookup"><span data-stu-id="af0a9-174">b.</span></span> <span data-ttu-id="af0a9-175">В текстовое поле **IdP Issuer** (Издатель IdP) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a9-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="af0a9-176">c.</span><span class="sxs-lookup"><span data-stu-id="af0a9-176">c.</span></span> <span data-ttu-id="af0a9-177">В текстовое поле **IdP Login URL** (URL-адрес входа IdP) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af0a9-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="af0a9-178">d.</span><span class="sxs-lookup"><span data-stu-id="af0a9-178">d.</span></span> <span data-ttu-id="af0a9-179">Вставьте значение **Отпечаток** с портала Azure в текстовое поле **Cert Fingerprint** (Отпечаток сертификата).</span><span class="sxs-lookup"><span data-stu-id="af0a9-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="af0a9-180">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="af0a9-181">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="af0a9-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="af0a9-182">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="af0a9-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="af0a9-183">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="af0a9-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="af0a9-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0a9-184">Create an Azure AD test user</span></span>
<span data-ttu-id="af0a9-185">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af0a9-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="af0a9-187">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="af0a9-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af0a9-188">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af0a9-190">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af0a9-192">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af0a9-194">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="af0a9-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af0a9-196">а.</span><span class="sxs-lookup"><span data-stu-id="af0a9-196">a.</span></span> <span data-ttu-id="af0a9-197">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af0a9-198">b.</span><span class="sxs-lookup"><span data-stu-id="af0a9-198">b.</span></span> <span data-ttu-id="af0a9-199">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af0a9-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af0a9-200">c.</span><span class="sxs-lookup"><span data-stu-id="af0a9-200">c.</span></span> <span data-ttu-id="af0a9-201">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="af0a9-202">d.</span><span class="sxs-lookup"><span data-stu-id="af0a9-202">d.</span></span> <span data-ttu-id="af0a9-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="af0a9-204">Создание тестового пользователя приложения Bonusly</span><span class="sxs-lookup"><span data-stu-id="af0a9-204">Create a Bonusly test user</span></span>

<span data-ttu-id="af0a9-205">Чтобы пользователи Azure AD могли входить в приложение Bonusly, они должны быть подготовлены в этом приложении.</span><span class="sxs-lookup"><span data-stu-id="af0a9-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="af0a9-206">В случае с Bonusly подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="af0a9-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="af0a9-207">Для подготовки учетных записей пользователей AAD можно использовать любые другие средства создания учетных записей пользователей Bonusly или API, предоставляемые разработчиками Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="af0a9-208">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="af0a9-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="af0a9-209">В окне браузера войдите в клиент Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="af0a9-210">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="af0a9-211">![Параметры](./media/active-directory-saas-bonus-tutorial/ic781041.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="af0a9-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="af0a9-212">Откройте вкладку **Users and bonuses** (Пользователи и бонусы).</span><span class="sxs-lookup"><span data-stu-id="af0a9-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="af0a9-213">![Пользователи и бонусы](./media/active-directory-saas-bonus-tutorial/ic781042.png "Пользователи и бонусы")</span><span class="sxs-lookup"><span data-stu-id="af0a9-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="af0a9-214">Выберите **Manage Users**(Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="af0a9-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="af0a9-215">![Управление пользователями](./media/active-directory-saas-bonus-tutorial/ic781043.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="af0a9-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="af0a9-216">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="af0a9-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="af0a9-217">![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781044.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="af0a9-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="af0a9-218">На странице **Добавление пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="af0a9-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="af0a9-219">![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781045.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="af0a9-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="af0a9-220">а.</span><span class="sxs-lookup"><span data-stu-id="af0a9-220">a.</span></span> <span data-ttu-id="af0a9-221">В текстовое поле **First name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="af0a9-222">b.</span><span class="sxs-lookup"><span data-stu-id="af0a9-222">b.</span></span> <span data-ttu-id="af0a9-223">В текстовое поле **Last name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="af0a9-224">c.</span><span class="sxs-lookup"><span data-stu-id="af0a9-224">c.</span></span> <span data-ttu-id="af0a9-225">В текстовое поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="af0a9-226">г)</span><span class="sxs-lookup"><span data-stu-id="af0a9-226">d.</span></span> <span data-ttu-id="af0a9-227">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="af0a9-228">Владелец учетной записи Azure AD получит сообщение электронной почты со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="af0a9-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="af0a9-229">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="af0a9-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="af0a9-230">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="af0a9-232">**Чтобы назначить пользователя Britta Simon в Bonusly, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="af0a9-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="af0a9-233">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="af0a9-235">В списке приложений выберите **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-235">In the applications list, select **Bonusly**.</span></span>

    ![Ссылка на Bonusly в списке "Приложения"](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="af0a9-237">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="af0a9-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-239">Click **Add** button.</span></span> <span data-ttu-id="af0a9-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="af0a9-242">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="af0a9-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af0a9-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="af0a9-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="af0a9-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="af0a9-245">Test single sign-on</span></span>

<span data-ttu-id="af0a9-246">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="af0a9-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="af0a9-247">Щелкнув элемент Bonusly на панели доступа, вы автоматически войдете в приложение Bonusly.</span><span class="sxs-lookup"><span data-stu-id="af0a9-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af0a9-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="af0a9-248">Additional resources</span></span>

* [<span data-ttu-id="af0a9-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af0a9-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af0a9-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af0a9-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

