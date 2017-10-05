---
title: "Руководство по интеграции Azure Active Directory с Learningpool Act | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="1e855-103">Руководство по интеграции Azure Active Directory с Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="1e855-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="1e855-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e855-105">Интеграция приложения Learningpool Act с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1e855-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e855-106">С помощью Azure AD вы можете контролировать доступ к Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="1e855-107">Вы можете включить автоматический вход пользователей в Learningpool Act (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e855-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e855-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1e855-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e855-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e855-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e855-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e855-110">Prerequisites</span></span>

<span data-ttu-id="1e855-111">Чтобы настроить интеграцию Azure AD с Learningpool Act, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1e855-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="1e855-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1e855-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e855-113">подписка с поддержкой единого входа Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e855-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1e855-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e855-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="1e855-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e855-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e855-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e855-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e855-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e855-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1e855-118">Scenario description</span></span>
<span data-ttu-id="1e855-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1e855-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e855-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="1e855-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e855-121">Добавление Learningpool Act из коллекции.</span><span class="sxs-lookup"><span data-stu-id="1e855-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="1e855-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e855-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="1e855-123">Добавление Learningpool Act из коллекции</span><span class="sxs-lookup"><span data-stu-id="1e855-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="1e855-124">Чтобы настроить интеграцию Learningpool Act с Azure AD, необходимо добавить Learningpool Act из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e855-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e855-125">**Чтобы добавить Learningpool Act из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1e855-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e855-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e855-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e855-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e855-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e855-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e855-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1e855-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="1e855-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1e855-133">В поле поиска введите **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="1e855-133">In the search box, type **Learningpool Act**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="1e855-135">На панели результатов выберите **Learningpool Act** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="1e855-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e855-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e855-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e855-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Learningpool Act с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e855-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e855-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Learningpool Act соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e855-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="1e855-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="1e855-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e855-142">Чтобы настроить и проверить единый вход Azure AD в Learningpool Act, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="1e855-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e855-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="1e855-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e855-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e855-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e855-145">**[Создание тестового пользователя Learningpool Act](#creating-a-learningpool-act-test-user)** требуется для создания в Learningpool Act пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e855-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e855-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e855-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e855-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1e855-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e855-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e855-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e855-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="1e855-150">**Чтобы настроить единый вход Azure AD в Learningpool Act, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1e855-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="1e855-151">На портале Azure на странице интеграции с приложением **Learningpool Act** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="1e855-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1e855-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="1e855-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="1e855-155">В разделе **Домены и URL-адреса приложения Learningpool Act** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1e855-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="1e855-157">а.</span><span class="sxs-lookup"><span data-stu-id="1e855-157">a.</span></span> <span data-ttu-id="1e855-158">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="1e855-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="1e855-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e855-159">b.</span></span> <span data-ttu-id="1e855-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="1e855-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="1e855-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1e855-161">These values are not real.</span></span> <span data-ttu-id="1e855-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="1e855-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e855-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="1e855-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="1e855-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e855-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="1e855-166">Приложение Learningpool Act ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="1e855-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1e855-167">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="1e855-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="1e855-168">Управлять значениями этих атрибутов можно на вкладке **"Атрибут"** приложения.</span><span class="sxs-lookup"><span data-stu-id="1e855-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="1e855-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="1e855-169">The following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="1e855-171">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1e855-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="1e855-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="1e855-172">Attribute Name</span></span> | <span data-ttu-id="1e855-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="1e855-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="1e855-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="1e855-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="1e855-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1e855-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="1e855-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="1e855-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="1e855-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1e855-177">user.givenname</span></span> |
    | <span data-ttu-id="1e855-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="1e855-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="1e855-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="1e855-179">user.mail</span></span> |    
    | <span data-ttu-id="1e855-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="1e855-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="1e855-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="1e855-181">user.surname</span></span> |
    
    <span data-ttu-id="1e855-182">а.</span><span class="sxs-lookup"><span data-stu-id="1e855-182">a.</span></span> <span data-ttu-id="1e855-183">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="1e855-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1e855-186">b.</span><span class="sxs-lookup"><span data-stu-id="1e855-186">b.</span></span> <span data-ttu-id="1e855-187">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="1e855-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="1e855-188">c.</span><span class="sxs-lookup"><span data-stu-id="1e855-188">c.</span></span> <span data-ttu-id="1e855-189">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="1e855-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="1e855-190">г)</span><span class="sxs-lookup"><span data-stu-id="1e855-190">d.</span></span> <span data-ttu-id="1e855-191">Оставьте пустым поле **Пространство имен**.</span><span class="sxs-lookup"><span data-stu-id="1e855-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="1e855-192">д.</span><span class="sxs-lookup"><span data-stu-id="1e855-192">e.</span></span> <span data-ttu-id="1e855-193">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1e855-193">Click **Ok**.</span></span>

7. <span data-ttu-id="1e855-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1e855-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1e855-196">Чтобы настроить единый вход на стороне **Learningpool Act**, отправьте в [службу поддержки Learningpool Act](https://www.Learningpool.com/support) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="1e855-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="1e855-197">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="1e855-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1e855-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="1e855-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e855-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1e855-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e855-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1e855-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e855-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e855-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e855-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e855-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1e855-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1e855-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e855-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e855-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e855-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1e855-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e855-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e855-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e855-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1e855-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e855-213">а.</span><span class="sxs-lookup"><span data-stu-id="1e855-213">a.</span></span> <span data-ttu-id="1e855-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e855-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e855-215">b.</span><span class="sxs-lookup"><span data-stu-id="1e855-215">b.</span></span> <span data-ttu-id="1e855-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e855-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e855-217">c.</span><span class="sxs-lookup"><span data-stu-id="1e855-217">c.</span></span> <span data-ttu-id="1e855-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="1e855-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e855-219">d.</span><span class="sxs-lookup"><span data-stu-id="1e855-219">d.</span></span> <span data-ttu-id="1e855-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1e855-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="1e855-221">Создание тестового пользователя Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="1e855-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="1e855-222">Чтобы разрешить пользователям Azure AD вход в Learningpool Act, они должны быть подготовлены для Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="1e855-223">Элемент действия для настройки подготовки пользователей в Learningpool Act отсутствует.</span><span class="sxs-lookup"><span data-stu-id="1e855-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="1e855-224">[Команда поддержки Learningpool Act](https://www.Learningpool.com/support) должна создать пользователей.</span><span class="sxs-lookup"><span data-stu-id="1e855-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="1e855-225">Вы можете использовать любые другие средства создания учетной записи пользователя Learningpool Act или API, предоставляемые Learningpool Act для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="1e855-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e855-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e855-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e855-227">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ей доступ к Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1e855-229">**Чтобы назначить пользователя Britta Simon в Learningpool Act, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="1e855-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="1e855-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1e855-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1e855-232">В списке приложений выберите **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="1e855-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="1e855-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e855-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1e855-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e855-236">Click **Add** button.</span></span> <span data-ttu-id="1e855-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1e855-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1e855-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e855-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e855-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1e855-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e855-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1e855-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e855-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1e855-242">Testing single sign-on</span></span>

<span data-ttu-id="1e855-243">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="1e855-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e855-244">Щелкнув элемент Learningpool Act на панели доступа, вы автоматически войдете в приложение Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="1e855-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e855-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e855-245">Additional resources</span></span>

* [<span data-ttu-id="1e855-246">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e855-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e855-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e855-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

