---
title: "Руководство по интеграции Azure Active Directory с Zendesk | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="cd266-103">Руководство. Интеграция Azure Active Directory с Zendesk</span><span class="sxs-lookup"><span data-stu-id="cd266-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="cd266-104">В этом руководстве описано, как интегрировать Zendesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd266-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd266-105">Интеграция Azure AD с приложением Zendesk обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="cd266-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd266-106">С помощью Azure AD вы можете контролировать доступ к Zendesk.</span><span class="sxs-lookup"><span data-stu-id="cd266-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="cd266-107">Вы можете включить автоматический вход пользователей в Zendesk (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd266-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd266-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cd266-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cd266-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd266-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd266-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd266-110">Prerequisites</span></span>

<span data-ttu-id="cd266-111">Чтобы настроить интеграцию Azure AD с Zendesk, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="cd266-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="cd266-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cd266-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd266-113">подписка Zendesk с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="cd266-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="cd266-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cd266-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cd266-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="cd266-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd266-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cd266-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd266-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd266-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cd266-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cd266-118">Scenario description</span></span>
<span data-ttu-id="cd266-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cd266-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd266-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="cd266-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd266-121">Добавление Zendesk из коллекции.</span><span class="sxs-lookup"><span data-stu-id="cd266-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="cd266-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd266-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="cd266-123">Добавление Zendesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="cd266-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="cd266-124">Чтобы настроить интеграцию Zendesk с Azure AD, необходимо добавить Zendesk из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cd266-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd266-125">**Чтобы добавить Zendesk из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="cd266-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd266-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd266-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd266-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="cd266-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd266-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cd266-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cd266-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="cd266-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cd266-133">В поле поиска введите **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="cd266-133">In the search box, type **Zendesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="cd266-135">На панели результатов выберите **Zendesk** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="cd266-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd266-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd266-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd266-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zendesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd266-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd266-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Zendesk соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd266-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="cd266-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Zendesk.</span><span class="sxs-lookup"><span data-stu-id="cd266-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="cd266-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zendesk.</span><span class="sxs-lookup"><span data-stu-id="cd266-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="cd266-142">Чтобы настроить и проверить единый вход Azure AD в Zendesk, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="cd266-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd266-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="cd266-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cd266-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd266-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd266-145">**[Создание тестового пользователя Zendesk](#creating-a-zendesk-test-user)** требуется для создания в Zendesk пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd266-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd266-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd266-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd266-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cd266-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd266-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd266-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd266-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Zendesk.</span><span class="sxs-lookup"><span data-stu-id="cd266-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="cd266-150">**Чтобы настроить единый вход Azure AD в Zendesk, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cd266-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="cd266-151">На портале Azure на странице интеграции с приложением **Zendesk** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="cd266-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cd266-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="cd266-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="cd266-155">В разделе **Домены и URL-адреса приложения Zendesk** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cd266-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="cd266-157">а.</span><span class="sxs-lookup"><span data-stu-id="cd266-157">a.</span></span> <span data-ttu-id="cd266-158">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<subdomain>.zendesk.com`.</span><span class="sxs-lookup"><span data-stu-id="cd266-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="cd266-159">b.</span><span class="sxs-lookup"><span data-stu-id="cd266-159">b.</span></span> <span data-ttu-id="cd266-160">В текстовом поле **Идентификатор** введите значение в следующем формате: `https://<subdomain>.zendesk.com`.</span><span class="sxs-lookup"><span data-stu-id="cd266-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd266-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cd266-161">These values are not real.</span></span> <span data-ttu-id="cd266-162">Замените эти значения фактическим URL-адресом для входа и URL-адресом идентификатора.</span><span class="sxs-lookup"><span data-stu-id="cd266-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="cd266-163">Чтобы получить эти значения, обратитесь в [службу поддержки Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise).</span><span class="sxs-lookup"><span data-stu-id="cd266-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="cd266-164">Приложение Zendesk ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="cd266-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cd266-165">Обязательные атрибуты SAML отсутствуют, но при необходимости можно добавить атрибут из раздела **Атрибуты пользователя**, выполнив следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cd266-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="cd266-167">а.</span><span class="sxs-lookup"><span data-stu-id="cd266-167">a.</span></span> <span data-ttu-id="cd266-168">Установите флажок **Просмотреть и изменить все другие атрибуты пользователей**.</span><span class="sxs-lookup"><span data-stu-id="cd266-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="cd266-170">b.</span><span class="sxs-lookup"><span data-stu-id="cd266-170">b.</span></span> <span data-ttu-id="cd266-171">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="cd266-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="cd266-173">c.</span><span class="sxs-lookup"><span data-stu-id="cd266-173">c.</span></span> <span data-ttu-id="cd266-174">В текстовом поле **Имя** введите имя атрибута (например, **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="cd266-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="cd266-175">г)</span><span class="sxs-lookup"><span data-stu-id="cd266-175">d.</span></span> <span data-ttu-id="cd266-176">В списке **Значение** выберите значение атрибута (например, **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="cd266-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="cd266-177">д.</span><span class="sxs-lookup"><span data-stu-id="cd266-177">e.</span></span> <span data-ttu-id="cd266-178">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cd266-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="cd266-179">Используйте атрибуты расширения для добавления атрибутов, которые отсутствуют в Azure AD по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cd266-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="cd266-180">Щелкните [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) (Атрибуты пользователя, которые можно настроить в SAML), чтобы получить полный список атрибутов SAML, которые принимает **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="cd266-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="cd266-181">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="cd266-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="cd266-183">В разделе **Настройка Zendesk** щелкните **Настроить Zendesk**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="cd266-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cd266-184">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="cd266-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="cd266-186">В другом окне браузера войдите на свой корпоративный сайт Zendesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="cd266-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="cd266-187">Щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="cd266-187">Click **Admin**.</span></span>

9. <span data-ttu-id="cd266-188">В области навигации слева щелкните **Settings** (Параметры), а затем щелкните **Security** (Безопасность).</span><span class="sxs-lookup"><span data-stu-id="cd266-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="cd266-189">На странице **Безопасность** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="cd266-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="cd266-190">![Безопасность](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="cd266-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="cd266-191">![Единый вход](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="cd266-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="cd266-192">а.</span><span class="sxs-lookup"><span data-stu-id="cd266-192">a.</span></span> <span data-ttu-id="cd266-193">Щелкните вкладку **Admin & Agents** (Администраторы и агенты).</span><span class="sxs-lookup"><span data-stu-id="cd266-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="cd266-194">b.</span><span class="sxs-lookup"><span data-stu-id="cd266-194">b.</span></span> <span data-ttu-id="cd266-195">Выберите **Single sign-on (SSO) and SAML** (Единый вход и SAML), а затем щелкните **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cd266-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="cd266-196">c.</span><span class="sxs-lookup"><span data-stu-id="cd266-196">c.</span></span> <span data-ttu-id="cd266-197">В текстовое поле **URL-адрес единого входа SAML** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cd266-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="cd266-198">г)</span><span class="sxs-lookup"><span data-stu-id="cd266-198">d.</span></span> <span data-ttu-id="cd266-199">В текстовое поле **URL-адрес удаленного выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cd266-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="cd266-200">д.</span><span class="sxs-lookup"><span data-stu-id="cd266-200">e.</span></span> <span data-ttu-id="cd266-201">В текстовое поле **Certificate Fingerprint** (Отпечаток сертификата) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cd266-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="cd266-202">f.</span><span class="sxs-lookup"><span data-stu-id="cd266-202">f.</span></span> <span data-ttu-id="cd266-203">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cd266-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd266-204">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd266-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd266-205">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd266-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cd266-207">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cd266-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd266-208">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd266-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd266-210">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="cd266-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd266-212">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="cd266-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd266-214">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cd266-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd266-216">а.</span><span class="sxs-lookup"><span data-stu-id="cd266-216">a.</span></span> <span data-ttu-id="cd266-217">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd266-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd266-218">b.</span><span class="sxs-lookup"><span data-stu-id="cd266-218">b.</span></span> <span data-ttu-id="cd266-219">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd266-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd266-220">c.</span><span class="sxs-lookup"><span data-stu-id="cd266-220">c.</span></span> <span data-ttu-id="cd266-221">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="cd266-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd266-222">d.</span><span class="sxs-lookup"><span data-stu-id="cd266-222">d.</span></span> <span data-ttu-id="cd266-223">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cd266-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="cd266-224">Создание тестового пользователя Zendesk</span><span class="sxs-lookup"><span data-stu-id="cd266-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="cd266-225">Чтобы пользователи Azure AD могли выполнять вход в **Zendesk**, они должны быть подготовлены для **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="cd266-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="cd266-226">В зависимости от роли, назначенной в приложениях, ожидаемое поведение будет следующим:</span><span class="sxs-lookup"><span data-stu-id="cd266-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="cd266-227">Учетные записи с ролью **Конечный пользователь** подготавливаются автоматически при входе.</span><span class="sxs-lookup"><span data-stu-id="cd266-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="cd266-228">Учетные записи с ролями **Агент** и **Администратор** необходимо вручную подготовить в **Zendesk** перед выполнением входа.</span><span class="sxs-lookup"><span data-stu-id="cd266-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="cd266-229">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cd266-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cd266-230">Войдите в клиент **Zendesk** .</span><span class="sxs-lookup"><span data-stu-id="cd266-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="cd266-231">Откройте вкладку **Список клиентов** .</span><span class="sxs-lookup"><span data-stu-id="cd266-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="cd266-232">Выберите вкладку **User** (Пользователь) и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="cd266-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="cd266-233">![Добавление пользователя](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="cd266-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="cd266-234">Введите электронный адрес существующей учетной записи Azure AD, которую необходимо подготовить, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cd266-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="cd266-235">![Новый пользователь](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="cd266-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="cd266-236">Вы можете использовать любые другие средства создания учетной записи пользователя Zendesk или API, предоставляемые Zendesk, для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="cd266-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd266-237">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd266-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd266-238">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Zendesk, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="cd266-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cd266-240">**Чтобы назначить пользователя Britta Simon в Zendesk, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cd266-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="cd266-241">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cd266-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cd266-243">В списке приложений выберите **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="cd266-243">In the applications list, select **Zendesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="cd266-245">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cd266-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cd266-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cd266-247">Click **Add** button.</span></span> <span data-ttu-id="cd266-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cd266-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cd266-250">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cd266-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cd266-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cd266-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd266-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cd266-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd266-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cd266-253">Testing single sign-on</span></span>

<span data-ttu-id="cd266-254">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="cd266-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cd266-255">Щелкнув элемент Zendesk на панели доступа, вы автоматически войдете в приложение Zendesk.</span><span class="sxs-lookup"><span data-stu-id="cd266-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="cd266-256">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd266-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd266-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cd266-257">Additional resources</span></span>

* [<span data-ttu-id="cd266-258">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd266-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd266-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd266-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
