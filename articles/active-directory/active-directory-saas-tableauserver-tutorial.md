---
title: "Руководство по интеграции Azure Active Directory с Tableau Server | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="b8bd2-103">Учебник. Интеграция Azure Active Directory с Tableau Server</span><span class="sxs-lookup"><span data-stu-id="b8bd2-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="b8bd2-104">В этом руководстве описано, как интегрировать Tableau Server с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8bd2-105">Интеграция Tableau Server с Azure AD дает приведенные далее преимущества:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8bd2-106">С помощью Azure AD вы можете контролировать доступ к Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="b8bd2-107">Вы можете включить автоматический вход пользователей в Tableau Server (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8bd2-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8bd2-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8bd2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8bd2-110">Prerequisites</span></span>

<span data-ttu-id="b8bd2-111">Чтобы настроить интеграцию Azure AD с приложением Tableau Server, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="b8bd2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b8bd2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8bd2-113">подписка Tableau Server с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8bd2-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8bd2-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8bd2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8bd2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8bd2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b8bd2-118">Scenario description</span></span>
<span data-ttu-id="b8bd2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8bd2-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8bd2-121">Добавление сервера Tableau Server из коллекции</span><span class="sxs-lookup"><span data-stu-id="b8bd2-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="b8bd2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8bd2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="b8bd2-123">Добавление сервера Tableau Server из коллекции</span><span class="sxs-lookup"><span data-stu-id="b8bd2-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="b8bd2-124">Чтобы настроить интеграцию Tableau Server с Azure AD, необходимо добавить Tableau Server из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8bd2-125">**Чтобы добавить Tableau Server из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8bd2-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8bd2-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8bd2-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8bd2-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b8bd2-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b8bd2-133">В поле поиска введите **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-133">In the search box, type **Tableau Server**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="b8bd2-135">На панели результатов выберите **Tableau Server** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8bd2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8bd2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8bd2-138">В этом разделе описана настройка и проверка единого входа Azure AD в Tableau Server для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8bd2-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Tableau Server соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="b8bd2-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="b8bd2-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8bd2-142">Чтобы настроить и проверить единый вход Azure AD в Tableau Server, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8bd2-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8bd2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8bd2-145">**[Создание тестового пользователя Tableau Server](#creating-a-tableau-server-test-user)** требуется для создания в Tableau Server пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8bd2-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8bd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8bd2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8bd2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8bd2-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="b8bd2-150">**Чтобы настроить единый вход Azure AD в Tableau Server, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8bd2-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="b8bd2-151">На портале Azure на странице интеграции с приложением **Tableau Server** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b8bd2-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="b8bd2-155">В разделе **Домены и URL-адреса Tableau Server** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="b8bd2-157">а.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-157">a.</span></span> <span data-ttu-id="b8bd2-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="b8bd2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="b8bd2-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-159">b.</span></span> <span data-ttu-id="b8bd2-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="b8bd2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="b8bd2-161">c.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-161">c.</span></span> <span data-ttu-id="b8bd2-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://azure.<domain name>.link/wg/saml/SSO/index.html`.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b8bd2-163">Приведенные выше значения используются только для примера.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-163">The preceding values are not real values.</span></span> <span data-ttu-id="b8bd2-164">Их необходимо заменить на фактические URL-адрес и идентификатор, которые можно найти на странице конфигурации Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="b8bd2-165">Приложение Tableau Server ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b8bd2-166">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-166">Configure the following claims for this application.</span></span> <span data-ttu-id="b8bd2-167">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="b8bd2-168">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-168">The following screenshot shows an example for the same.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="b8bd2-170">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b8bd2-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="b8bd2-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b8bd2-171">Attribute Name</span></span> | <span data-ttu-id="b8bd2-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b8bd2-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="b8bd2-173">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="b8bd2-173">username</span></span> | <span data-ttu-id="b8bd2-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="b8bd2-174">*user.displayname*</span></span> |

    <span data-ttu-id="b8bd2-175">а.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-175">a.</span></span> <span data-ttu-id="b8bd2-176">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="b8bd2-179">b.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-179">b.</span></span> <span data-ttu-id="b8bd2-180">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b8bd2-181">c.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-181">c.</span></span> <span data-ttu-id="b8bd2-182">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b8bd2-183">d.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-183">d.</span></span> <span data-ttu-id="b8bd2-184">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-184">Click **Ok**</span></span>


6. <span data-ttu-id="b8bd2-185">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="b8bd2-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b8bd2-187">Click **Save** button.</span></span>

    <span data-ttu-id="b8bd2-188">![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="b8bd2-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="b8bd2-189">Чтобы единый вход был настроен для вашего приложения, войдите в клиент Tableau Server с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="b8bd2-190">а.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-190">a.</span></span> <span data-ttu-id="b8bd2-191">В окне конфигурации Tableau Server откройте вкладку **SAML** .</span><span class="sxs-lookup"><span data-stu-id="b8bd2-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="b8bd2-193">b.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-193">b.</span></span> <span data-ttu-id="b8bd2-194">Установите флажок **Использовать SAML для единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="b8bd2-195">c.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-195">c.</span></span> <span data-ttu-id="b8bd2-196">URL-адрес возврата Tableau Server — URL-адрес для доступа пользователей Tableau Server, например http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="b8bd2-197">Мы не рекомендуем использовать http://localhost.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="b8bd2-198">URL-адреса с конечной косой чертой (например http://tableau_server/) не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="b8bd2-199">Скопируйте **URL-адрес возврата Tableau Server** и вставьте его в текстовое поле **URL-адрес входа** Azure AD в разделе **Домены и URL-адреса Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="b8bd2-200">г)</span><span class="sxs-lookup"><span data-stu-id="b8bd2-200">d.</span></span> <span data-ttu-id="b8bd2-201">Идентификатор сущности SAML — идентификатор сущности однозначно определяет установку Tableau Server для поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="b8bd2-202">Если нужно, здесь можно еще раз ввести URL-адрес Tableau Server, но это необязательно должен быть URL-адрес Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="b8bd2-203">Скопируйте **Идентификатор сущности SAML** и вставьте его в текстовое поле **Идентификатор** Azure AD в разделе **Домены и URL-адреса Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="b8bd2-204">д.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-204">e.</span></span> <span data-ttu-id="b8bd2-205">Нажмите кнопку **Экспортировать файл метаданных** и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="b8bd2-206">Найдите URL-адрес службы обработчика утверждений с Http Post и индексом 0 и скопируйте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="b8bd2-207">Вставьте его в текстовое поле **URL-адрес ответа** в разделе **Домены и URL-адреса Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="b8bd2-208">Е.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-208">f.</span></span> <span data-ttu-id="b8bd2-209">Найдите файл метаданных федерации, скачанный с портала Azure, и отправьте его в разделе **файл метаданных поставщика удостоверений SAML**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="b8bd2-210">g.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-210">g.</span></span> <span data-ttu-id="b8bd2-211">Нажмите кнопку **ОК** на странице конфигурации Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="b8bd2-212">Клиенту необходимо отправить любой сертификат во время настройки единого входа SAML Tableau Server, и этот сертификат будет проигнорирован в потоке единого входа.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="b8bd2-213">Более подробные сведения о настройке SAML в Tableau Server см. в статье о [настройке SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="b8bd2-214">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8bd2-215">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8bd2-216">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8bd2-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8bd2-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8bd2-218">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b8bd2-220">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8bd2-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8bd2-221">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8bd2-223">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8bd2-225">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8bd2-227">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8bd2-229">а.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-229">a.</span></span> <span data-ttu-id="b8bd2-230">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8bd2-231">b.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-231">b.</span></span> <span data-ttu-id="b8bd2-232">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8bd2-233">c.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-233">c.</span></span> <span data-ttu-id="b8bd2-234">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8bd2-235">d.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-235">d.</span></span> <span data-ttu-id="b8bd2-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="b8bd2-237">Создание тестового пользователя Tableau Server</span><span class="sxs-lookup"><span data-stu-id="b8bd2-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="b8bd2-238">Цель этого раздела — создать в приложении Tableau Server пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="b8bd2-239">Необходимо подготовить всех пользователей в приложении Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="b8bd2-240">Имя пользователя должно совпадать со значением, настроенным в пользовательском атрибуте Azure AD **username**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="b8bd2-241">В случае правильного сопоставления интеграция должна обеспечить [настройку единого входа в Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="b8bd2-242">Если необходимо создать пользователя вручную, обратитесь к администратору Tableau Server в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8bd2-243">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8bd2-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8bd2-244">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b8bd2-246">**Чтобы назначить пользователя Britta Simon в Tableau Server, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8bd2-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="b8bd2-247">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b8bd2-249">В списке приложений выберите **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-249">In the applications list, select **Tableau Server**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="b8bd2-251">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b8bd2-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-253">Click **Add** button.</span></span> <span data-ttu-id="b8bd2-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b8bd2-256">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8bd2-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8bd2-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8bd2-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b8bd2-259">Testing single sign-on</span></span>

<span data-ttu-id="b8bd2-260">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8bd2-261">Щелкнув элемент Tableau Server на панели доступа, вы автоматически войдете в приложение Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b8bd2-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="b8bd2-262">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b8bd2-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b8bd2-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b8bd2-263">Additional resources</span></span>

* [<span data-ttu-id="b8bd2-264">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8bd2-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8bd2-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8bd2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

