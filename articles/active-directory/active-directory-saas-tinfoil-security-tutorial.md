---
title: "Руководство по интеграции Azure Active Directory с TINFOIL SECURITY | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="e8b41-103">Руководство по интеграции Azure Active Directory с TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="e8b41-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="e8b41-104">В этом руководстве описано, как интегрировать TINFOIL SECURITY с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8b41-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8b41-105">Интеграция TINFOIL SECURITY с Azure AD имеет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e8b41-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8b41-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="e8b41-107">Вы можете включить автоматический вход пользователей в TINFOIL SECURITY (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8b41-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8b41-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e8b41-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8b41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8b41-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e8b41-110">Prerequisites</span></span>

<span data-ttu-id="e8b41-111">Чтобы настроить интеграцию Azure AD с приложением TINFOIL SECURITY, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e8b41-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="e8b41-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e8b41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8b41-113">подписка TINFOIL SECURITY с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e8b41-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8b41-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e8b41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8b41-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e8b41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8b41-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e8b41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8b41-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8b41-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8b41-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e8b41-118">Scenario description</span></span>
<span data-ttu-id="e8b41-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e8b41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8b41-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e8b41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8b41-121">Добавление TINFOIL SECURITY из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e8b41-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="e8b41-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8b41-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="e8b41-123">Добавление TINFOIL SECURITY из коллекции</span><span class="sxs-lookup"><span data-stu-id="e8b41-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="e8b41-124">Чтобы настроить интеграцию TINFOIL SECURITY с Azure AD, вам нужно добавить TINFOIL SECURITY из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e8b41-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8b41-125">**Чтобы добавить TINFOIL SECURITY из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="e8b41-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8b41-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8b41-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8b41-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e8b41-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e8b41-133">В поле поиска введите **TINFOIL SECURITY**, выберите **TINFOIL SECURITY** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e8b41-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![Добавление TINFOIL SECURITY из коллекции](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e8b41-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8b41-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e8b41-136">В этом разделе описана настройка и проверка единого входа Azure AD в TINFOIL SECURITY с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8b41-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8b41-137">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в TINFOIL SECURITY соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8b41-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="e8b41-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="e8b41-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e8b41-140">Чтобы настроить и проверить единый вход Azure AD в TINFOIL SECURITY, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8b41-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8b41-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e8b41-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8b41-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8b41-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8b41-143">**[Создание тестового пользователя TINFOIL SECURITY](#create-a-tinfoil-security-test-user)** требуется для того, чтобы в TINFOIL SECURITY существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8b41-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8b41-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8b41-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8b41-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e8b41-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e8b41-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8b41-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e8b41-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="e8b41-148">**Чтобы настроить единый вход Azure AD в TINFOIL SECURITY, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="e8b41-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="e8b41-149">На портале Azure на странице интеграции с приложением **TINFOIL SECURITY** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e8b41-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e8b41-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Вход на основе SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="e8b41-153">В разделе **Домены и URL-адреса приложения TINFOIL SECURITY** не нужно выполнять никаких действий, так как это приложение предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b41-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="e8b41-155">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="e8b41-157">Чтобы добавить обязательные сопоставления атрибутов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8b41-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="e8b41-158">![Атрибуты](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="e8b41-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="e8b41-159">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="e8b41-159">Attribute Name</span></span>    |   <span data-ttu-id="e8b41-160">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="e8b41-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e8b41-161">accountid</span><span class="sxs-lookup"><span data-stu-id="e8b41-161">accountid</span></span> | <span data-ttu-id="e8b41-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="e8b41-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="e8b41-163">а.</span><span class="sxs-lookup"><span data-stu-id="e8b41-163">a.</span></span> <span data-ttu-id="e8b41-164">Щелкните **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="e8b41-165">![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="e8b41-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="e8b41-166">![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="e8b41-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="e8b41-167">b.</span><span class="sxs-lookup"><span data-stu-id="e8b41-167">b.</span></span> <span data-ttu-id="e8b41-168">В текстовом поле **Имя атрибута** введите **accountid**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="e8b41-169">c.</span><span class="sxs-lookup"><span data-stu-id="e8b41-169">c.</span></span> <span data-ttu-id="e8b41-170">В текстовое поле **Значение атрибута** следует вставить идентификатор учетной записи, который вы получите позже при работе с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="e8b41-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="e8b41-171">г)</span><span class="sxs-lookup"><span data-stu-id="e8b41-171">d.</span></span> <span data-ttu-id="e8b41-172">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="e8b41-173">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e8b41-173">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e8b41-175">В разделе **Конфигурация TINFOIL SECURITY** щелкните **Настроить TINFOIL SECURITY**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e8b41-176">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="e8b41-178">В другом окне веб-браузера войдите на свой корпоративный веб-сайт TINFOIL SECURITY в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e8b41-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="e8b41-179">На панели инструментов в верхней части экрана щелкните **Моя учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="e8b41-180">![Панель мониторинга](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Панель мониторинга")</span><span class="sxs-lookup"><span data-stu-id="e8b41-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="e8b41-181">Выберите пункт **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-181">Click **Security**.</span></span>
   
    <span data-ttu-id="e8b41-182">![Безопасность](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="e8b41-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="e8b41-183">На странице настроек **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8b41-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="e8b41-184">![Единый вход](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="e8b41-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="e8b41-185">а.</span><span class="sxs-lookup"><span data-stu-id="e8b41-185">a.</span></span> <span data-ttu-id="e8b41-186">Выберите **Включить SAML**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="e8b41-187">b.</span><span class="sxs-lookup"><span data-stu-id="e8b41-187">b.</span></span> <span data-ttu-id="e8b41-188">Щелкните **Настроить вручную**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="e8b41-189">c.</span><span class="sxs-lookup"><span data-stu-id="e8b41-189">c.</span></span> <span data-ttu-id="e8b41-190">В текстовое поле **SAML Post URL** (URL-адрес POST SAML) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b41-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="e8b41-191">г)</span><span class="sxs-lookup"><span data-stu-id="e8b41-191">d.</span></span> <span data-ttu-id="e8b41-192">В текстовое поле **SAML Certificate Fingerprint** (Отпечаток сертификата SAML) вставьте значение **Отпечаток**, скопированное в разделе **Сертификат подписи SAML**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="e8b41-193">д.</span><span class="sxs-lookup"><span data-stu-id="e8b41-193">e.</span></span> <span data-ttu-id="e8b41-194">Скопируйте значение **Your Account ID** (Ваш идентификатор учетной записи) и вставьте его в текстовое поле **Значение атрибута** в разделе **Добавление атрибута** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b41-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="e8b41-195">f.</span><span class="sxs-lookup"><span data-stu-id="e8b41-195">f.</span></span> <span data-ttu-id="e8b41-196">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e8b41-197">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e8b41-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e8b41-198">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e8b41-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e8b41-199">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e8b41-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e8b41-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8b41-200">Create an Azure AD test user</span></span>
<span data-ttu-id="e8b41-201">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8b41-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e8b41-203">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e8b41-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8b41-204">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8b41-206">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="e8b41-207">Выберите "Пользователи и группы" > "Все пользователи".</span><span class="sxs-lookup"><span data-stu-id="e8b41-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8b41-208">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Пользователь](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8b41-210">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8b41-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8b41-212">а.</span><span class="sxs-lookup"><span data-stu-id="e8b41-212">a.</span></span> <span data-ttu-id="e8b41-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8b41-214">b.</span><span class="sxs-lookup"><span data-stu-id="e8b41-214">b.</span></span> <span data-ttu-id="e8b41-215">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8b41-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8b41-216">c.</span><span class="sxs-lookup"><span data-stu-id="e8b41-216">c.</span></span> <span data-ttu-id="e8b41-217">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e8b41-218">d.</span><span class="sxs-lookup"><span data-stu-id="e8b41-218">d.</span></span> <span data-ttu-id="e8b41-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="e8b41-220">Создание тестового пользователя TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="e8b41-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="e8b41-221">Чтобы пользователи Azure AD могли выполнить вход в TINFOIL SECURITY, они должны быть подготовлены для TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="e8b41-222">В случае TINFOIL SECURITY подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e8b41-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="e8b41-223">**Чтобы подготовить пользователя, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e8b41-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="e8b41-224">Если пользователь является частью учетной записи Enterprise, то для создания учетной записи пользователя необходимо обратиться к [группе поддержки TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact).</span><span class="sxs-lookup"><span data-stu-id="e8b41-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="e8b41-225">Если пользователь является обычным пользователем SaaS TINFOIL SECURITY, то он может добавить участника совместной работы на любой из своих сайтов.</span><span class="sxs-lookup"><span data-stu-id="e8b41-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="e8b41-226">Это активирует процесс, который отправит приглашение по указанному электронному адресу для создания учетной записи пользователя TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="e8b41-227">Вы можете использовать любые другие инструменты создания учетных записей пользователя TINFOIL SECURITY или API, предоставляемые TINFOIL SECURITY для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8b41-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e8b41-228">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8b41-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="e8b41-229">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e8b41-231">**Чтобы назначить пользователя Britta Simon в TINFOIL SECURITY, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e8b41-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="e8b41-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e8b41-234">Из списка приложений выберите **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![Выбор TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="e8b41-236">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e8b41-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-238">Click **Add** button.</span></span> <span data-ttu-id="e8b41-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e8b41-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8b41-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8b41-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e8b41-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e8b41-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e8b41-244">Test single sign-on</span></span>

<span data-ttu-id="e8b41-245">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e8b41-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8b41-246">Щелкнув элемент "TINFOIL SECURITY" на панели доступа, вы автоматически войдете в приложение TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="e8b41-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="e8b41-247">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e8b41-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8b41-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8b41-248">Additional resources</span></span>

* [<span data-ttu-id="e8b41-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8b41-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8b41-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8b41-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

