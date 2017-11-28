---
title: "Руководство по интеграции Azure Active Directory с myPolicies | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="b6898-103">Руководство по интеграции Azure Active Directory с myPolicies</span><span class="sxs-lookup"><span data-stu-id="b6898-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="b6898-104">В этом руководстве описано, как интегрировать приложение myPolicies с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6898-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6898-105">Интеграция Azure AD с приложением myPolicies обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b6898-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6898-106">С помощью Azure AD вы можете контролировать доступ к myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="b6898-107">Вы можете включить автоматический вход пользователей в myPolicies (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6898-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6898-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b6898-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6898-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6898-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6898-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6898-110">Prerequisites</span></span>

<span data-ttu-id="b6898-111">Чтобы настроить интеграцию Azure AD с myPolicies, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b6898-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="b6898-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b6898-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6898-113">подписка myPolicies с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6898-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6898-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b6898-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6898-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b6898-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6898-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b6898-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6898-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6898-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6898-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b6898-118">Scenario description</span></span>
<span data-ttu-id="b6898-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b6898-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6898-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b6898-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6898-121">Добавление myPolicies из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b6898-121">Adding myPolicies from the gallery</span></span>
2. <span data-ttu-id="b6898-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6898-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="b6898-123">Добавление myPolicies из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6898-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="b6898-124">Чтобы настроить интеграцию myPolicies с Azure AD, необходимо добавить myPolicies из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b6898-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6898-125">**Чтобы добавить myPolicies из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="b6898-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6898-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6898-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6898-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6898-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6898-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6898-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b6898-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b6898-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b6898-133">В поле поиска введите **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="b6898-133">In the search box, type **myPolicies**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="b6898-135">На панели результатов выберите **myPolicies** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="b6898-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6898-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6898-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6898-138">В этом разделе описана настройка и проверка единого входа Azure AD в myPolicies с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6898-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b6898-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в myPolicies соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6898-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="b6898-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="b6898-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6898-142">Чтобы настроить и проверить единый вход Azure AD в myPolicies, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b6898-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6898-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b6898-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6898-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6898-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6898-145">**[Создание тестового пользователя myPolicies](#creating-a-mypolicies-test-user)** требуется для того, чтобы в myPolicies существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6898-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6898-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6898-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6898-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b6898-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6898-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6898-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6898-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="b6898-150">**Чтобы настроить единый вход Azure AD в myPolicies, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="b6898-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="b6898-151">На портале Azure на странице интеграции с приложением **myPolicies** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b6898-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b6898-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6898-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="b6898-155">В разделе **Домены и URL-адреса приложения myPolicies** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b6898-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="b6898-157">а.</span><span class="sxs-lookup"><span data-stu-id="b6898-157">a.</span></span> <span data-ttu-id="b6898-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="b6898-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="b6898-159">b.</span><span class="sxs-lookup"><span data-stu-id="b6898-159">b.</span></span> <span data-ttu-id="b6898-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="b6898-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6898-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b6898-161">These values are not real.</span></span> <span data-ttu-id="b6898-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="b6898-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b6898-163">Чтобы получить эти значения, обратитесь к [группе поддержки myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="b6898-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

4. <span data-ttu-id="b6898-164">Приложение myPolicies ожидает утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="b6898-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b6898-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b6898-165">Configure the following claims for this application.</span></span> <span data-ttu-id="b6898-166">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="b6898-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b6898-167">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="b6898-167">The following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="b6898-169">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей**, чтобы развернуть атрибуты.</span><span class="sxs-lookup"><span data-stu-id="b6898-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="b6898-170">Выполните следующие действия для каждого отображаемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="b6898-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="b6898-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b6898-171">Attribute Name</span></span> | <span data-ttu-id="b6898-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b6898-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="b6898-173">givenname</span><span class="sxs-lookup"><span data-stu-id="b6898-173">givenname</span></span> | <span data-ttu-id="b6898-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b6898-174">user.givenname</span></span> |
    | <span data-ttu-id="b6898-175">surname</span><span class="sxs-lookup"><span data-stu-id="b6898-175">surname</span></span> | <span data-ttu-id="b6898-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="b6898-176">user.surname</span></span> |
    | <span data-ttu-id="b6898-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="b6898-177">emailaddress</span></span> | <span data-ttu-id="b6898-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="b6898-178">user.mail</span></span> |
    | <span data-ttu-id="b6898-179">name</span><span class="sxs-lookup"><span data-stu-id="b6898-179">name</span></span> | <span data-ttu-id="b6898-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b6898-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="b6898-181">а.</span><span class="sxs-lookup"><span data-stu-id="b6898-181">a.</span></span> <span data-ttu-id="b6898-182">Щелкните атрибут, чтобы открыть диалоговое окно **Изменить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="b6898-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b6898-184">b.</span><span class="sxs-lookup"><span data-stu-id="b6898-184">b.</span></span> <span data-ttu-id="b6898-185">Удалите значение URL-адреса из **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="b6898-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="b6898-186">c.</span><span class="sxs-lookup"><span data-stu-id="b6898-186">c.</span></span> <span data-ttu-id="b6898-187">Нажмите кнопку **ОК**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="b6898-187">Click **Ok** to save the setting.</span></span>
    
6. <span data-ttu-id="b6898-188">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6898-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="b6898-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b6898-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b6898-192">В разделе **Конфигурация myPolicies** щелкните **Настроить myPolicies**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b6898-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6898-193">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b6898-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="b6898-195">Чтобы настроить единый вход на стороне **myPolicies**, нужно отправить скачанный **сертификат в кодировке Base64** и **URL-адрес службы единого входа SAML** [группе поддержки myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="b6898-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="b6898-196">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b6898-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6898-197">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b6898-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6898-198">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b6898-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6898-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6898-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6898-200">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6898-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b6898-202">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b6898-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6898-203">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6898-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6898-205">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b6898-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6898-207">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6898-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6898-209">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6898-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6898-211">а.</span><span class="sxs-lookup"><span data-stu-id="b6898-211">a.</span></span> <span data-ttu-id="b6898-212">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6898-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6898-213">b.</span><span class="sxs-lookup"><span data-stu-id="b6898-213">b.</span></span> <span data-ttu-id="b6898-214">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6898-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6898-215">c.</span><span class="sxs-lookup"><span data-stu-id="b6898-215">c.</span></span> <span data-ttu-id="b6898-216">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b6898-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6898-217">d.</span><span class="sxs-lookup"><span data-stu-id="b6898-217">d.</span></span> <span data-ttu-id="b6898-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b6898-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="b6898-219">Создание тестового пользователя myPolicies</span><span class="sxs-lookup"><span data-stu-id="b6898-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="b6898-220">В этом разделе описано, как создать пользователя Britta Simon в myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="b6898-221">Обратитесь к [группе поддержки myPolicies](mailto:support@mypolicies.com), чтобы добавить пользователей на платформу myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="b6898-222">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="b6898-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6898-223">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6898-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6898-224">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b6898-226">**Чтобы назначить пользователя Britta Simon в myPolicies, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="b6898-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="b6898-227">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6898-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b6898-229">Из списка приложений выберите **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="b6898-229">In the applications list, select **myPolicies**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="b6898-231">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6898-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b6898-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6898-233">Click **Add** button.</span></span> <span data-ttu-id="b6898-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6898-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b6898-236">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b6898-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6898-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b6898-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6898-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b6898-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6898-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b6898-239">Testing single sign-on</span></span>

<span data-ttu-id="b6898-240">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b6898-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b6898-241">Щелкнув элемент "myPolicies" на панели доступа, вы автоматически войдете в приложение myPolicies.</span><span class="sxs-lookup"><span data-stu-id="b6898-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="b6898-242">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6898-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6898-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6898-243">Additional resources</span></span>

* [<span data-ttu-id="b6898-244">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6898-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6898-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6898-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

