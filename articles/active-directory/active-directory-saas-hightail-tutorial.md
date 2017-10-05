---
title: "Учебник. Интеграция Azure Active Directory с Hightail | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="3eb4c-103">Учебник. Интеграция Azure Active Directory с Hightail</span><span class="sxs-lookup"><span data-stu-id="3eb4c-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="3eb4c-104">В этом учебнике описано, как интегрировать приложение Hightail с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3eb4c-105">Интеграция Hightail с Azure AD дает приведенные далее преимущества:</span><span class="sxs-lookup"><span data-stu-id="3eb4c-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3eb4c-106">С помощью Azure AD вы можете контролировать доступ к Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="3eb4c-107">Вы можете включить автоматический вход пользователей в Hightail (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3eb4c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3eb4c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eb4c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3eb4c-110">Prerequisites</span></span>

<span data-ttu-id="3eb4c-111">Чтобы настроить интеграцию Azure AD с Hightail, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3eb4c-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="3eb4c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3eb4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3eb4c-113">подписка Hightail с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3eb4c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3eb4c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3eb4c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3eb4c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3eb4c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3eb4c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3eb4c-118">Scenario description</span></span>
<span data-ttu-id="3eb4c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3eb4c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3eb4c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3eb4c-121">Добавление Hightail из коллекции</span><span class="sxs-lookup"><span data-stu-id="3eb4c-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="3eb4c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="3eb4c-123">Добавление Hightail из коллекции</span><span class="sxs-lookup"><span data-stu-id="3eb4c-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="3eb4c-124">Чтобы настроить интеграцию Hightail с Azure AD, необходимо добавить Hightail из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3eb4c-125">**Чтобы добавить Hightail из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3eb4c-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb4c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3eb4c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3eb4c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3eb4c-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3eb4c-133">В поле поиска введите **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-133">In the search box, type **Hightail**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="3eb4c-135">На панели результатов выберите **Hightail** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3eb4c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3eb4c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Hightail с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3eb4c-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Hightail соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="3eb4c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="3eb4c-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3eb4c-142">Чтобы настроить и проверить единый вход Azure AD в Hightail, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="3eb4c-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3eb4c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3eb4c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3eb4c-145">**[Создание тестового пользователя Hightail](#creating-a-hightail-test-user)** требуется для создания в Hightail пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3eb4c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3eb4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3eb4c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3eb4c-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="3eb4c-150">**Чтобы настроить единый вход Azure AD в Hightail, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3eb4c-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb4c-151">На портале Azure на странице интеграции с приложением **Hightail** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3eb4c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="3eb4c-155">В разделе **Домен и URL-адреса приложения Hightail** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="3eb4c-157">В текстовом поле **URL-адрес ответа** введите URL-адрес следующим образом: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3eb4c-158">Приведенное выше значение используется только для примера.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-158">The preceding value is not real value.</span></span> <span data-ttu-id="3eb4c-159">Вы замените это значение на фактический URL-адрес ответа, который описывается далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="3eb4c-160">В разделе **Домен и URL-адреса приложения Hightail** выполните следующие действия, если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="3eb4c-162">а.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-162">a.</span></span> <span data-ttu-id="3eb4c-163">Щелкните **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3eb4c-164">b.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-164">b.</span></span> <span data-ttu-id="3eb4c-165">В текстовом поле **URL-адрес для входа** введите следующий URL-адрес: `https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="3eb4c-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="3eb4c-166">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="3eb4c-168">Приложение Hightail ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3eb4c-169">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="3eb4c-170">Управлять значениями этих атрибутов можно на вкладке **"Атрибут"** приложения.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="3eb4c-171">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-171">The following screenshot shows an example for this.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="3eb4c-173">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3eb4c-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="3eb4c-174">Attribute Name</span></span> | <span data-ttu-id="3eb4c-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="3eb4c-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="3eb4c-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="3eb4c-176">FirstName</span></span> | <span data-ttu-id="3eb4c-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3eb4c-177">user.givenname</span></span> |
    | <span data-ttu-id="3eb4c-178">LastName</span><span class="sxs-lookup"><span data-stu-id="3eb4c-178">LastName</span></span> | <span data-ttu-id="3eb4c-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="3eb4c-179">user.surname</span></span> |
    | <span data-ttu-id="3eb4c-180">Email</span><span class="sxs-lookup"><span data-stu-id="3eb4c-180">Email</span></span> | <span data-ttu-id="3eb4c-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="3eb4c-181">user.mail</span></span> |    
    | <span data-ttu-id="3eb4c-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="3eb4c-182">UserIdentity</span></span> | <span data-ttu-id="3eb4c-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="3eb4c-183">user.mail</span></span> |
    
    <span data-ttu-id="3eb4c-184">а.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-184">a.</span></span> <span data-ttu-id="3eb4c-185">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="3eb4c-188">b.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-188">b.</span></span> <span data-ttu-id="3eb4c-189">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3eb4c-190">c.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-190">c.</span></span> <span data-ttu-id="3eb4c-191">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3eb4c-192">г)</span><span class="sxs-lookup"><span data-stu-id="3eb4c-192">d.</span></span> <span data-ttu-id="3eb4c-193">Оставьте пустым поле **Пространство имен**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="3eb4c-194">д.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-194">e.</span></span> <span data-ttu-id="3eb4c-195">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-195">Click **Ok**.</span></span>

7. <span data-ttu-id="3eb4c-196">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3eb4c-196">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3eb4c-198">В разделе **Конфигурация Hightail** щелкните **Настроить Hightail**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3eb4c-199">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="3eb4c-201">Перед настройкой единого входа в приложение Hightail внесите почтовый домен Hightail в список разрешенных, чтобы все пользователи этого домена могли использовать функции единого входа.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="3eb4c-202">Чтобы единый вход был настроен для вашего приложения, войдите в клиент Hightail с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="3eb4c-203">а.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-203">a.</span></span> <span data-ttu-id="3eb4c-204">В меню в верхней части экрана откройте вкладку **Account** (Учетная запись) и выберите **Configure SAML** (Настроить SAML).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="3eb4c-206">b.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-206">b.</span></span> <span data-ttu-id="3eb4c-207">Установите флажок **Включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="3eb4c-209">c.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-209">c.</span></span> <span data-ttu-id="3eb4c-210">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат подписывания токена SAML**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="3eb4c-212">г)</span><span class="sxs-lookup"><span data-stu-id="3eb4c-212">d.</span></span> <span data-ttu-id="3eb4c-213">В текстовое поле **Центр SAML (поставщик удостоверений)** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="3eb4c-215">д.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-215">e.</span></span> <span data-ttu-id="3eb4c-216">Чтобы настроить приложение в **режиме, инициированном поставщиком удостоверений**, выберите **Identity Provider (IdP) initiated log in** (Вход, инициированный поставщиком удостоверений (IdP)).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="3eb4c-217">Чтобы настроить приложение в **режиме, инициированном поставщиком услуг**, выберите **Service Provider (SP) initiated log in** (Вход, инициированный поставщиком услуг (SP)).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="3eb4c-219">f.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-219">f.</span></span> <span data-ttu-id="3eb4c-220">Скопируйте URL-адрес получателя SAML для своего экземпляра и вставьте его в текстовое поле **URL-адрес ответа** в разделе **Домен и URL-адреса приложения Hightail** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="3eb4c-221">ж.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-221">g.</span></span> <span data-ttu-id="3eb4c-222">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3eb4c-223">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3eb4c-224">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3eb4c-225">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3eb4c-226">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb4c-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="3eb4c-227">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3eb4c-229">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3eb4c-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb4c-230">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3eb4c-232">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3eb4c-234">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3eb4c-236">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3eb4c-238">а.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-238">a.</span></span> <span data-ttu-id="3eb4c-239">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3eb4c-240">b.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-240">b.</span></span> <span data-ttu-id="3eb4c-241">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3eb4c-242">c.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-242">c.</span></span> <span data-ttu-id="3eb4c-243">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3eb4c-244">d.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-244">d.</span></span> <span data-ttu-id="3eb4c-245">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="3eb4c-246">Создание тестового пользователя Hightail</span><span class="sxs-lookup"><span data-stu-id="3eb4c-246">Creating a Hightail test user</span></span>

<span data-ttu-id="3eb4c-247">Цель этого раздела — создать пользователя с именем Britta Simon в Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="3eb4c-248">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-248">There is no action item for you in this section.</span></span> <span data-ttu-id="3eb4c-249">Приложение Hightail поддерживает JIT-подготовку пользователей на основе настраиваемых утверждений.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="3eb4c-250">Если вы настроили пользовательские утверждения, как показано в разделе **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** выше, пользователь будет автоматически создан в приложении (если он еще не существует).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="3eb4c-251">Если нужно создать пользователя вручную, обратитесь в [службу поддержки Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="3eb4c-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3eb4c-252">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb4c-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3eb4c-253">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3eb4c-255">**Чтобы назначить пользователя Britta Simon в Hightail, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3eb4c-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb4c-256">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3eb4c-258">В списке приложений выберите **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-258">In the applications list, select **Hightail**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="3eb4c-260">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3eb4c-262">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-262">Click **Add** button.</span></span> <span data-ttu-id="3eb4c-263">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3eb4c-265">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3eb4c-266">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3eb4c-267">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3eb4c-268">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3eb4c-268">Testing single sign-on</span></span>

<span data-ttu-id="3eb4c-269">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3eb4c-270">Щелкнув элемент Hightail на панели доступа, вы автоматически войдете в приложение Hightail.</span><span class="sxs-lookup"><span data-stu-id="3eb4c-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3eb4c-271">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3eb4c-271">Additional resources</span></span>

* [<span data-ttu-id="3eb4c-272">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eb4c-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3eb4c-273">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3eb4c-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

