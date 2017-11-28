---
title: "Руководство по интеграции Azure Active Directory с Boomi | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="9a6c0-103">Руководство. Интеграция Azure Active Directory с Boomi</span><span class="sxs-lookup"><span data-stu-id="9a6c0-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="9a6c0-104">В этом руководстве описано, как интегрировать Boomi с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a6c0-105">Интеграция Azure AD с приложением Boomi обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a6c0-106">С помощью Azure AD вы можете контролировать доступ к Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="9a6c0-107">Вы можете включить автоматический вход пользователей в Boomi (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a6c0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a6c0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a6c0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a6c0-110">Prerequisites</span></span>

<span data-ttu-id="9a6c0-111">Чтобы настроить интеграцию Azure AD с Boomi, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9a6c0-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="9a6c0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9a6c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a6c0-113">Подписка с поддержкой единого входа Boomi</span><span class="sxs-lookup"><span data-stu-id="9a6c0-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a6c0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a6c0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9a6c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a6c0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a6c0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a6c0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9a6c0-118">Scenario description</span></span>
<span data-ttu-id="9a6c0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a6c0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9a6c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a6c0-121">Добавление Boomi из коллекции</span><span class="sxs-lookup"><span data-stu-id="9a6c0-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="9a6c0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a6c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="9a6c0-123">Добавление Boomi из коллекции</span><span class="sxs-lookup"><span data-stu-id="9a6c0-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="9a6c0-124">Чтобы настроить интеграцию Boomi с Azure AD, необходимо добавить Boomi из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a6c0-125">**Чтобы добавить Boomi из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a6c0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a6c0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a6c0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9a6c0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9a6c0-133">В поле поиска введите **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-133">In the search box, type **Boomi**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="9a6c0-135">На панели результатов выберите **Boomi** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a6c0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a6c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a6c0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Boomi с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a6c0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Boomi соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="9a6c0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="9a6c0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9a6c0-142">Чтобы настроить и проверить единый вход Azure AD в Boomi, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a6c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a6c0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a6c0-145">**[Создание тестового пользователя Boomi](#creating-a-boomi-test-user)** требуется для создания в Boomi пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a6c0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a6c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a6c0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a6c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a6c0-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="9a6c0-150">**Чтобы настроить единый вход Azure AD в Boomi, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="9a6c0-151">На портале Azure на странице интеграции с приложением **Boomi** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9a6c0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="9a6c0-155">В разделе **Домены и URL-адреса приложения Boomi** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9a6c0-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="9a6c0-157">а.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-157">a.</span></span> <span data-ttu-id="9a6c0-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="9a6c0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="9a6c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-159">b.</span></span> <span data-ttu-id="9a6c0-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://platform.boomi.com/sso/<accountname>/saml`.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a6c0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-161">These values are not real.</span></span> <span data-ttu-id="9a6c0-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9a6c0-163">Чтобы получить это значение, обратитесь в [службу поддержки Boomi](https://boomi.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="9a6c0-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="9a6c0-166">Приложение Boomi ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9a6c0-167">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="9a6c0-168">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9a6c0-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-169">The following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="9a6c0-171">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** для каждой строки в таблице ниже выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="9a6c0-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="9a6c0-172">Attribute Name</span></span> | <span data-ttu-id="9a6c0-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="9a6c0-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="9a6c0-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="9a6c0-174">FEDERATION_ID</span></span> | <span data-ttu-id="9a6c0-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="9a6c0-175">user.mail</span></span> |
    
    <span data-ttu-id="9a6c0-176">а.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-176">a.</span></span> <span data-ttu-id="9a6c0-177">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="9a6c0-180">b.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-180">b.</span></span> <span data-ttu-id="9a6c0-181">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9a6c0-182">c.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-182">c.</span></span> <span data-ttu-id="9a6c0-183">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9a6c0-184">г)</span><span class="sxs-lookup"><span data-stu-id="9a6c0-184">d.</span></span> <span data-ttu-id="9a6c0-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-185">Click **Ok**.</span></span>

6. <span data-ttu-id="9a6c0-186">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9a6c0-186">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9a6c0-188">В разделе **Настройка Boomi** щелкните **Настроить Boomi**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9a6c0-189">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="9a6c0-191">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Boomi в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="9a6c0-192">Перейдите к пункту **Company Name** (Название компании) и выберите **Set up** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="9a6c0-193">Щелкните вкладку **SSO Options** (Параметры единого входа) и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9a6c0-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="9a6c0-195">а.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-195">a.</span></span> <span data-ttu-id="9a6c0-196">Установите флажок **Enable SAML Single Sign-On** (Разрешить единый вход SAML).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="9a6c0-197">b.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-197">b.</span></span> <span data-ttu-id="9a6c0-198">Щелкните **Import** (Импорт), чтобы передать сертификат, загруженный из Azure AD, в качестве **сертификата поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="9a6c0-199">c.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-199">c.</span></span> <span data-ttu-id="9a6c0-200">В текстовом поле **URL-адрес для входа поставщика удостоверений** введите значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) из окна настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="9a6c0-201">г)</span><span class="sxs-lookup"><span data-stu-id="9a6c0-201">d.</span></span> <span data-ttu-id="9a6c0-202">Для параметра **Federation Id Location** (Расположение идентификатора федерации) выберите переключатель **Federation Id is in FEDERATION_ID Attribute element** (Идентификатор федерации передается в элементе атрибута FEDERATION_ID).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="9a6c0-203">д.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-203">e.</span></span> <span data-ttu-id="9a6c0-204">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="9a6c0-205">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a6c0-206">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a6c0-207">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a6c0-208">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a6c0-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a6c0-209">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9a6c0-211">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a6c0-212">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a6c0-214">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a6c0-216">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a6c0-218">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a6c0-220">а.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-220">a.</span></span> <span data-ttu-id="9a6c0-221">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a6c0-222">b.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-222">b.</span></span> <span data-ttu-id="9a6c0-223">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a6c0-224">c.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-224">c.</span></span> <span data-ttu-id="9a6c0-225">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a6c0-226">d.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-226">d.</span></span> <span data-ttu-id="9a6c0-227">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="9a6c0-228">Создание тестового пользователя Boomi</span><span class="sxs-lookup"><span data-stu-id="9a6c0-228">Creating a Boomi test user</span></span>

<span data-ttu-id="9a6c0-229">Чтобы пользователи Azure AD могли выполнять вход в Boomi, они должны быть подготовлены для Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="9a6c0-230">В случае с Boomi подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="9a6c0-231">Чтобы подготовить учетную запись пользователя, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="9a6c0-232">Войдите на корпоративный сайт Boomi в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="9a6c0-233">После входа в систему, перейдите к разделу **User Management** (Управление пользователями) и найдите элемент **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="9a6c0-234">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="9a6c0-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="9a6c0-235">Щелкните значок **+**. Откроется диалоговое окно **Add/Maintain User Roles** (Добавить или настроить роли пользователей).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="9a6c0-236">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="9a6c0-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="9a6c0-237">![Пользователи](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="9a6c0-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="9a6c0-238">а.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-238">a.</span></span> <span data-ttu-id="9a6c0-239">В текстовом поле **User e-mail address** (Адрес электронной почты пользователя) введите электронный адрес пользователя, например BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="9a6c0-240">b.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-240">b.</span></span> <span data-ttu-id="9a6c0-241">В текстовом поле **First name** (Имя) введите имя пользователя, например Britta.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="9a6c0-242">c.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-242">c.</span></span> <span data-ttu-id="9a6c0-243">В текстовом поле **Last name** (Фамилия) введите фамилию, предположим, Simon.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="9a6c0-244">г)</span><span class="sxs-lookup"><span data-stu-id="9a6c0-244">d.</span></span> <span data-ttu-id="9a6c0-245">Введите **идентификатор федерации** пользователя.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="9a6c0-246">Каждый пользователь должен иметь уникальный идентификатор федерации в пределах учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="9a6c0-247">д.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-247">e.</span></span> <span data-ttu-id="9a6c0-248">Назначьте для пользователя роль **Standard User** (Обычный пользователь).</span><span class="sxs-lookup"><span data-stu-id="9a6c0-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="9a6c0-249">Не назначайте роль администратора, так как она не только обеспечивает возможность единого входа, но и предоставляет и обычный доступ к Atmosphere.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="9a6c0-250">f.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-250">f.</span></span> <span data-ttu-id="9a6c0-251">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9a6c0-252">Пользователь не получит по электронной почте сообщение с паролем для входа в учетную запись AtomSphere. Вместо этого управление паролем осуществляется через поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="9a6c0-253">Вы можете использовать для создания учетной записи Boomi любые другие средства или интерфейсы API, которые Boomi предоставляет для подготовки учетных записей AAD.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a6c0-254">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a6c0-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a6c0-255">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Boomi, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9a6c0-257">**Чтобы назначить пользователя Britta Simon в Boomi, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9a6c0-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="9a6c0-258">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9a6c0-260">В списке приложений выберите **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-260">In the applications list, select **Boomi**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="9a6c0-262">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9a6c0-264">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-264">Click **Add** button.</span></span> <span data-ttu-id="9a6c0-265">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9a6c0-267">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a6c0-268">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a6c0-269">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a6c0-270">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9a6c0-270">Testing single sign-on</span></span>

<span data-ttu-id="9a6c0-271">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a6c0-272">Щелкнув элемент Boomi на панели доступа, вы автоматически войдете в приложение Boomi.</span><span class="sxs-lookup"><span data-stu-id="9a6c0-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a6c0-273">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9a6c0-273">Additional resources</span></span>

* [<span data-ttu-id="9a6c0-274">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a6c0-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a6c0-275">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a6c0-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

