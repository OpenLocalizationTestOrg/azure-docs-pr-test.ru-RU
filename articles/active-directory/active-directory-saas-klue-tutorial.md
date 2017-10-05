---
title: "Руководство по интеграции Azure Active Directory с Klue | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c64417c136340b3ffa5d67c618c6fe037d2992b5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="3ce21-103">Руководство по интеграции Azure Active Directory с Klue</span><span class="sxs-lookup"><span data-stu-id="3ce21-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="3ce21-104">В этом руководстве описано, как интегрировать Klue с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ce21-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ce21-105">Интеграция Azure AD с приложением Klue обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3ce21-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ce21-106">С помощью Azure AD вы можете контролировать доступ к Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="3ce21-107">Вы можете включить автоматический вход пользователей в Klue (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ce21-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ce21-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce21-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ce21-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ce21-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ce21-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3ce21-110">Prerequisites</span></span>

<span data-ttu-id="3ce21-111">Чтобы настроить интеграцию Azure AD с Klue, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3ce21-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="3ce21-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3ce21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ce21-113">подписка Klue с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3ce21-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ce21-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3ce21-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ce21-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3ce21-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ce21-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3ce21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ce21-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ce21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ce21-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3ce21-118">Scenario description</span></span>
<span data-ttu-id="3ce21-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3ce21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ce21-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3ce21-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ce21-121">Добавление Klue из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3ce21-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="3ce21-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ce21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="3ce21-123">Добавление Klue из коллекции</span><span class="sxs-lookup"><span data-stu-id="3ce21-123">Adding Klue from the gallery</span></span>
<span data-ttu-id="3ce21-124">Чтобы настроить интеграцию Klue с Azure AD, необходимо добавить Klue из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3ce21-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ce21-125">**Чтобы добавить Klue из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3ce21-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ce21-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ce21-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ce21-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3ce21-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3ce21-133">В поле поиска введите **Klue**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-133">In the search box, type **Klue**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="3ce21-135">На панели результатов выберите **Klue** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3ce21-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ce21-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ce21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ce21-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Klue с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ce21-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ce21-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Klue соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ce21-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="3ce21-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="3ce21-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ce21-142">Чтобы настроить и проверить единый вход Azure AD в Klue, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3ce21-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ce21-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3ce21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ce21-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ce21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ce21-145">**[Создание тестового пользователя Klue](#creating-a-klue-test-user)** требуется для того, чтобы в Klue существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ce21-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ce21-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ce21-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ce21-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3ce21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ce21-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ce21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ce21-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="3ce21-150">**Чтобы настроить единый вход Azure AD в Klue, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3ce21-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="3ce21-151">На портале Azure на странице интеграции с приложением **Klue** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3ce21-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3ce21-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="3ce21-155">Если вы хотите настроить приложение в режиме, инициируемом **IdP**, то в разделе **Домены и URL-адреса приложения Klue** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ce21-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="3ce21-157">а.</span><span class="sxs-lookup"><span data-stu-id="3ce21-157">a.</span></span> <span data-ttu-id="3ce21-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="3ce21-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="3ce21-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ce21-159">b.</span></span> <span data-ttu-id="3ce21-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`.</span><span class="sxs-lookup"><span data-stu-id="3ce21-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="3ce21-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="3ce21-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="3ce21-162">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="3ce21-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="3ce21-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3ce21-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3ce21-165">These values are not real.</span></span> <span data-ttu-id="3ce21-166">Укажите вместо них фактические значения URL-адреса ответа, идентификатора и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="3ce21-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="3ce21-167">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="3ce21-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="3ce21-168">Приложение Klue ожидает утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="3ce21-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="3ce21-169">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="3ce21-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="3ce21-171">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ce21-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3ce21-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="3ce21-172">Attribute Name</span></span>      | <span data-ttu-id="3ce21-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="3ce21-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="3ce21-174">first_name</span><span class="sxs-lookup"><span data-stu-id="3ce21-174">first_name</span></span>          | <span data-ttu-id="3ce21-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3ce21-175">user.givenname</span></span> |
    | <span data-ttu-id="3ce21-176">last_name</span><span class="sxs-lookup"><span data-stu-id="3ce21-176">last_name</span></span>           | <span data-ttu-id="3ce21-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="3ce21-177">user.surname</span></span> |
    | <span data-ttu-id="3ce21-178">email</span><span class="sxs-lookup"><span data-stu-id="3ce21-178">email</span></span>               | <span data-ttu-id="3ce21-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="3ce21-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="3ce21-180">а.</span><span class="sxs-lookup"><span data-stu-id="3ce21-180">a.</span></span> <span data-ttu-id="3ce21-181">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3ce21-184">b.</span><span class="sxs-lookup"><span data-stu-id="3ce21-184">b.</span></span> <span data-ttu-id="3ce21-185">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="3ce21-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3ce21-186">c.</span><span class="sxs-lookup"><span data-stu-id="3ce21-186">c.</span></span> <span data-ttu-id="3ce21-187">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="3ce21-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3ce21-188">г)</span><span class="sxs-lookup"><span data-stu-id="3ce21-188">d.</span></span> <span data-ttu-id="3ce21-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-189">Click **Ok**.</span></span>

7. <span data-ttu-id="3ce21-190">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3ce21-190">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="3ce21-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3ce21-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="3ce21-194">В разделе **Конфигурация Klue** щелкните **Настроить Klue**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-194">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ce21-195">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="3ce21-197">Чтобы настроить единый вход на стороне **Klue**, нужно отправить скачанный **сертификат в кодировке Base64, URL-адрес службы единого входа SAML и идентификатор сущности SAML** [группе поддержки Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="3ce21-197">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="3ce21-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3ce21-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ce21-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3ce21-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ce21-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3ce21-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ce21-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ce21-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ce21-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ce21-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3ce21-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3ce21-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ce21-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ce21-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ce21-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ce21-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ce21-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ce21-213">а.</span><span class="sxs-lookup"><span data-stu-id="3ce21-213">a.</span></span> <span data-ttu-id="3ce21-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ce21-215">b.</span><span class="sxs-lookup"><span data-stu-id="3ce21-215">b.</span></span> <span data-ttu-id="3ce21-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ce21-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ce21-217">c.</span><span class="sxs-lookup"><span data-stu-id="3ce21-217">c.</span></span> <span data-ttu-id="3ce21-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ce21-219">d.</span><span class="sxs-lookup"><span data-stu-id="3ce21-219">d.</span></span> <span data-ttu-id="3ce21-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="3ce21-221">Создание тестового пользователя Klue</span><span class="sxs-lookup"><span data-stu-id="3ce21-221">Creating a Klue test user</span></span>

<span data-ttu-id="3ce21-222">Цель этого раздела — создать пользователя с именем Britta Simon в Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-222">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="3ce21-223">Приложение Klue поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ce21-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3ce21-224">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="3ce21-224">There is no action item for you in this section.</span></span> <span data-ttu-id="3ce21-225">Пользователь будет создан при попытке получить доступ к приложению Klue (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="3ce21-225">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="3ce21-226">Чтобы создать пользователя вручную, обратитесь к [группе поддержки Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="3ce21-226">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ce21-227">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ce21-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ce21-228">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3ce21-230">**Чтобы назначить пользователя Britta Simon в Klue, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3ce21-230">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="3ce21-231">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3ce21-233">Из списка приложений выберите **Klue**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-233">In the applications list, select **Klue**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="3ce21-235">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3ce21-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-237">Click **Add** button.</span></span> <span data-ttu-id="3ce21-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3ce21-240">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ce21-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ce21-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3ce21-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ce21-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3ce21-243">Testing single sign-on</span></span>

<span data-ttu-id="3ce21-244">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3ce21-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ce21-245">Щелкнув элемент "Klue" на панели доступа, вы автоматически войдете в приложение Klue.</span><span class="sxs-lookup"><span data-stu-id="3ce21-245">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="3ce21-246">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ce21-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ce21-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3ce21-247">Additional resources</span></span>

* [<span data-ttu-id="3ce21-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ce21-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ce21-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ce21-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

