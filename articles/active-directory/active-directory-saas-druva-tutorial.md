---
title: "Руководство по интеграции Azure Active Directory с Druva | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="29929-103">Руководство по интеграции Azure Active Directory с Druva</span><span class="sxs-lookup"><span data-stu-id="29929-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="29929-104">В этом руководстве описано, как интегрировать Druva с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29929-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29929-105">Интеграция Azure AD с приложением Druva обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="29929-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29929-106">С помощью Azure AD вы можете контролировать доступ к Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="29929-107">Вы можете включить автоматический вход пользователей в Druva (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29929-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29929-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="29929-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="29929-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29929-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29929-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="29929-110">Prerequisites</span></span>

<span data-ttu-id="29929-111">Чтобы настроить интеграцию Azure AD с Druva, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="29929-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="29929-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="29929-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29929-113">Подписка с поддержкой единого входа Druva</span><span class="sxs-lookup"><span data-stu-id="29929-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29929-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="29929-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29929-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="29929-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29929-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="29929-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29929-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29929-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29929-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="29929-118">Scenario description</span></span>
<span data-ttu-id="29929-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="29929-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29929-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="29929-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29929-121">Добавление Druva из коллекции</span><span class="sxs-lookup"><span data-stu-id="29929-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="29929-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29929-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="29929-123">Добавление Druva из коллекции</span><span class="sxs-lookup"><span data-stu-id="29929-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="29929-124">Чтобы настроить интеграцию Druva с Azure AD, необходимо добавить Druva из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="29929-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29929-125">**Чтобы добавить Druva из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29929-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29929-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29929-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="29929-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="29929-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29929-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29929-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="29929-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="29929-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="29929-133">В поле поиска введите **Druva**, выберите **Druva** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="29929-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva в списке результатов](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29929-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29929-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29929-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Druva с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29929-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29929-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Druva соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29929-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="29929-138">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="29929-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29929-140">Чтобы настроить и проверить единый вход Azure AD в Druva, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="29929-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29929-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="29929-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29929-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29929-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29929-143">**[Создание тестового пользователя Druva](#create-a-druva-test-user)** требуется для того, чтобы в Druva существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29929-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29929-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29929-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29929-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="29929-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29929-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="29929-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29929-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="29929-148">**Чтобы настроить единый вход Azure AD в Druva, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29929-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="29929-149">На портале Azure на странице интеграции с приложением **Druva** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="29929-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="29929-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="29929-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="29929-153">В разделе **Домены и URL-адреса приложения Druva** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="29929-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="29929-155">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="29929-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="29929-156">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="29929-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="29929-158">Приложение Druva ожидает проверочные утверждения SAML в определенном формате, поэтому в вашу конфигурацию **атрибутов токена SAML** следует добавить сопоставления настраиваемых атрибутов.</span><span class="sxs-lookup"><span data-stu-id="29929-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="29929-160">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29929-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="29929-161">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="29929-161">Attribute Name</span></span>      | <span data-ttu-id="29929-162">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="29929-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="29929-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="29929-163">insync\_auth\_token</span></span> |<span data-ttu-id="29929-164">Введите созданное значение маркера</span><span class="sxs-lookup"><span data-stu-id="29929-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="29929-165">а.</span><span class="sxs-lookup"><span data-stu-id="29929-165">a.</span></span> <span data-ttu-id="29929-166">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="29929-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="29929-169">b.</span><span class="sxs-lookup"><span data-stu-id="29929-169">b.</span></span> <span data-ttu-id="29929-170">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="29929-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="29929-171">c.</span><span class="sxs-lookup"><span data-stu-id="29929-171">c.</span></span> <span data-ttu-id="29929-172">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="29929-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="29929-173">Созданное значение маркера описано далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="29929-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="29929-174">d.</span><span class="sxs-lookup"><span data-stu-id="29929-174">d.</span></span> <span data-ttu-id="29929-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="29929-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="29929-176">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="29929-176">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="29929-178">В разделе **Конфигурация Druva** щелкните **Настроить Druva**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="29929-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29929-179">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="29929-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="29929-181">В другом окне браузера войдите на свой корпоративный веб-сайт Druva с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="29929-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="29929-182">Последовательно выберите **Manage \> Settings** (Управление > Параметры).</span><span class="sxs-lookup"><span data-stu-id="29929-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="29929-183">![Параметры](./media/active-directory-saas-druva-tutorial/ic795091.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="29929-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="29929-184">В диалоговом окне «Параметры единого входа» выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29929-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="29929-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings") (Параметры единого входа)</span><span class="sxs-lookup"><span data-stu-id="29929-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="29929-186">а.</span><span class="sxs-lookup"><span data-stu-id="29929-186">a.</span></span> <span data-ttu-id="29929-187">Вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure, в текстовое поле **ID Provider Login URL** (URL-адрес входа поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="29929-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="29929-188">b.</span><span class="sxs-lookup"><span data-stu-id="29929-188">b.</span></span> <span data-ttu-id="29929-189">Вставьте **URL-адрес выхода**, скопированный на портале Azure, в текстовое поле **ID Provider Logout URL** (URL-адрес выхода поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="29929-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="29929-190">c.</span><span class="sxs-lookup"><span data-stu-id="29929-190">c.</span></span> <span data-ttu-id="29929-191">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат поставщика удостоверений** .</span><span class="sxs-lookup"><span data-stu-id="29929-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="29929-192">d.</span><span class="sxs-lookup"><span data-stu-id="29929-192">d.</span></span> <span data-ttu-id="29929-193">Чтобы открыть страницу **Параметры**, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="29929-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="29929-194">На странице **Параметры** щелкните **Generate SSO Token** (Создать маркер единого входа).</span><span class="sxs-lookup"><span data-stu-id="29929-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="29929-195">![Параметры](./media/active-directory-saas-druva-tutorial/ic795093.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="29929-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="29929-196">В диалоговом окне **Токен проверки подлинности единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29929-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="29929-197">![Маркер единого входа](./media/active-directory-saas-druva-tutorial/ic795094.png "Маркер единого входа")</span><span class="sxs-lookup"><span data-stu-id="29929-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="29929-198">а.</span><span class="sxs-lookup"><span data-stu-id="29929-198">a.</span></span> <span data-ttu-id="29929-199">Нажмите кнопку **Копировать**, затем вставьте скопированное значение в текстовое поле **Значение** в разделе **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="29929-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="29929-200">b.</span><span class="sxs-lookup"><span data-stu-id="29929-200">b.</span></span> <span data-ttu-id="29929-201">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="29929-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="29929-202">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="29929-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29929-203">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="29929-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29929-204">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="29929-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29929-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29929-205">Create an Azure AD test user</span></span>

<span data-ttu-id="29929-206">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29929-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="29929-208">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="29929-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29929-209">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29929-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29929-211">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="29929-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29929-213">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29929-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29929-215">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="29929-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29929-217">а.</span><span class="sxs-lookup"><span data-stu-id="29929-217">a.</span></span> <span data-ttu-id="29929-218">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29929-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29929-219">b.</span><span class="sxs-lookup"><span data-stu-id="29929-219">b.</span></span> <span data-ttu-id="29929-220">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29929-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="29929-221">c.</span><span class="sxs-lookup"><span data-stu-id="29929-221">c.</span></span> <span data-ttu-id="29929-222">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="29929-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="29929-223">г)</span><span class="sxs-lookup"><span data-stu-id="29929-223">d.</span></span> <span data-ttu-id="29929-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29929-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="29929-225">Создание тестового пользователя Druva</span><span class="sxs-lookup"><span data-stu-id="29929-225">Create a Druva test user</span></span>

<span data-ttu-id="29929-226">Чтобы пользователи Azure AD могли выполнять вход в Druva, они должны быть подготовлены для Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="29929-227">В случае с Druva подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="29929-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="29929-228">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="29929-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="29929-229">Выполните вход на веб-сайт компании **Druva** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="29929-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="29929-230">Выберите **Manage \> Users** (Управление > Пользователи).</span><span class="sxs-lookup"><span data-stu-id="29929-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="29929-231">![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795097.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="29929-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="29929-232">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29929-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="29929-233">![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795098.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="29929-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="29929-234">В диалоговом окне «Создание пользователя» выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29929-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="29929-235">![Создание пользователя](./media/active-directory-saas-druva-tutorial/ic795099.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="29929-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="29929-236">а.</span><span class="sxs-lookup"><span data-stu-id="29929-236">a.</span></span> <span data-ttu-id="29929-237">В текстовое поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="29929-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="29929-238">b.</span><span class="sxs-lookup"><span data-stu-id="29929-238">b.</span></span> <span data-ttu-id="29929-239">В текстовое поле **Name** (Имя) введите имя, например **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29929-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="29929-240">c.</span><span class="sxs-lookup"><span data-stu-id="29929-240">c.</span></span> <span data-ttu-id="29929-241">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="29929-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="29929-242">Вы можете использовать любые другие средства для создания учетной записи пользователя Druva или API, предоставляемые Druva для подготовки учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29929-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29929-243">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29929-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="29929-244">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="29929-246">**Чтобы назначить пользователя Britta Simon в Druva, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29929-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="29929-247">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29929-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="29929-249">В списке приложений выберите **Druva**.</span><span class="sxs-lookup"><span data-stu-id="29929-249">In the applications list, select **Druva**.</span></span>

    ![Ссылка на Druva в списке "Приложения"](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="29929-251">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29929-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="29929-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29929-253">Click **Add** button.</span></span> <span data-ttu-id="29929-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29929-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="29929-256">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29929-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29929-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="29929-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29929-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="29929-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29929-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="29929-259">Test single sign-on</span></span>

<span data-ttu-id="29929-260">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="29929-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29929-261">Щелкнув плитку Druva на панели доступа, вы автоматически войдете в приложение Druva.</span><span class="sxs-lookup"><span data-stu-id="29929-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="29929-262">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29929-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29929-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="29929-263">Additional resources</span></span>

* [<span data-ttu-id="29929-264">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29929-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29929-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29929-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

