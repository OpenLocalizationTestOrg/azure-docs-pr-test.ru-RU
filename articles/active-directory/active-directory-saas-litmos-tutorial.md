---
title: "Учебник. Интеграция Azure Active Directory с Litmos | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="5b7c2-103">Руководство по интеграции Azure Active Directory с Litmos</span><span class="sxs-lookup"><span data-stu-id="5b7c2-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="5b7c2-104">В этом руководстве описано, как интегрировать приложение Litmos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b7c2-105">Интеграция Azure AD с приложением Litmos обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b7c2-106">С помощью Azure AD вы можете контролировать доступ к Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="5b7c2-107">Вы можете включить автоматический вход пользователей в Litmos (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5b7c2-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5b7c2-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b7c2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5b7c2-110">Prerequisites</span></span>

<span data-ttu-id="5b7c2-111">Чтобы настроить интеграцию Azure AD с Litmos, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5b7c2-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="5b7c2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5b7c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b7c2-113">подписка Litmos с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b7c2-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b7c2-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5b7c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b7c2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b7c2-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b7c2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5b7c2-118">Scenario description</span></span>
<span data-ttu-id="5b7c2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b7c2-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5b7c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b7c2-121">Добавление Litmos из коллекции</span><span class="sxs-lookup"><span data-stu-id="5b7c2-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="5b7c2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="5b7c2-123">Добавление Litmos из коллекции</span><span class="sxs-lookup"><span data-stu-id="5b7c2-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="5b7c2-124">Чтобы настроить интеграцию Litmos с Azure AD, необходимо добавить Litmos из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b7c2-125">**Чтобы добавить Litmos из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5b7c2-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b7c2-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="5b7c2-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b7c2-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="5b7c2-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="5b7c2-133">В поле поиска введите **Litmos**, выберите **Litmos** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos в списке результатов](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b7c2-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7c2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5b7c2-136">В этом разделе описана настройка и проверка единого входа Azure AD в Litmos с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b7c2-137">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Litmos соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="5b7c2-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="5b7c2-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b7c2-140">Чтобы настроить и проверить единый вход Azure AD в Litmos, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b7c2-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b7c2-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b7c2-143">**[Создание тестового пользователя Litmos](#create-a-litmos-test-user)** требуется для того, чтобы в Litmos существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b7c2-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b7c2-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b7c2-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7c2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b7c2-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="5b7c2-148">**Чтобы настроить единый вход Azure AD в Litmos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5b7c2-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5b7c2-149">На портале Azure на странице интеграции с приложением **Litmos** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="5b7c2-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="5b7c2-153">В разделе **Домены и URL-адреса приложения Litmos** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="5b7c2-155">а.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-155">a.</span></span> <span data-ttu-id="5b7c2-156">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="5b7c2-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="5b7c2-157">b.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-157">b.</span></span> <span data-ttu-id="5b7c2-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.litmos.com/integration/samllogin`.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b7c2-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-159">These values are not real.</span></span> <span data-ttu-id="5b7c2-160">Вместо этих значений укажите фактические идентификатор и URL-адрес ответа, к которым мы вернемся позже в этом руководстве, или обратитесь к [группе поддержки Litmos](https://www.litmos.com/contact-us/), чтобы получить данные значения.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="5b7c2-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="5b7c2-163">В рамках конфигурации необходимо настроить **атрибуты токена SAML** для приложения Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Раздел "Атрибут"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="5b7c2-165">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="5b7c2-165">Attribute Name</span></span>   | <span data-ttu-id="5b7c2-166">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="5b7c2-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="5b7c2-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="5b7c2-167">FirstName</span></span> |<span data-ttu-id="5b7c2-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5b7c2-168">user.givenname</span></span> |
    | <span data-ttu-id="5b7c2-169">LastName</span><span class="sxs-lookup"><span data-stu-id="5b7c2-169">LastName</span></span>  |<span data-ttu-id="5b7c2-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="5b7c2-170">user.surname</span></span> |
    | <span data-ttu-id="5b7c2-171">Email</span><span class="sxs-lookup"><span data-stu-id="5b7c2-171">Email</span></span> |<span data-ttu-id="5b7c2-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="5b7c2-172">user.mail</span></span> |

    <span data-ttu-id="5b7c2-173">а.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-173">a.</span></span> <span data-ttu-id="5b7c2-174">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Добавление атрибута](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно "Добавление атрибута"](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5b7c2-177">b.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-177">b.</span></span> <span data-ttu-id="5b7c2-178">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5b7c2-179">c.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-179">c.</span></span> <span data-ttu-id="5b7c2-180">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5b7c2-181">г)</span><span class="sxs-lookup"><span data-stu-id="5b7c2-181">d.</span></span> <span data-ttu-id="5b7c2-182">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="5b7c2-183">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5b7c2-183">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5b7c2-185">В другом окне браузера войдите на корпоративный сайт Litmos в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="5b7c2-186">В области навигации слева щелкните **Accounts**(Учетные записи).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

9. <span data-ttu-id="5b7c2-188">Щелкните вкладку **Integrations** (Интеграции).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-188">Click the **Integrations** tab.</span></span>
   
    ![Вкладка "Integrations" (Интеграция)][23] 

10. <span data-ttu-id="5b7c2-190">На вкладке **Integrations** (Интеграции) прокрутите страницу вниз до раздела **3rd Party Integrations** (Интеграции сторонних поставщиков), а затем откройте вкладку **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Раздел "SAML 2.0"][24] 

11. <span data-ttu-id="5b7c2-192">Скопируйте значение в разделе **The SAML endpoint for litmos is** (Конечная точка SAML для Litmos) и вставьте его в текстовое поле **URL-адрес ответа** в разделе **Домены и URL-адреса приложения Litmos** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Конечная точка SAML][26] 

12. <span data-ttu-id="5b7c2-194">В приложении **Litmos** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Приложение Litmos][25] 
     
     <span data-ttu-id="5b7c2-196">а.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-196">a.</span></span> <span data-ttu-id="5b7c2-197">Выберите команду **Enable SAML**(Включить SAML).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="5b7c2-198">b.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-198">b.</span></span> <span data-ttu-id="5b7c2-199">Откройте сертификат в кодировке Base 64 в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **SAML X.509 Certificate** (Сертификат SAML X.509).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="5b7c2-200">c.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-200">c.</span></span> <span data-ttu-id="5b7c2-201">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5b7c2-202">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b7c2-203">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b7c2-204">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b7c2-205">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7c2-205">Create an Azure AD test user</span></span>

<span data-ttu-id="5b7c2-206">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="5b7c2-208">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5b7c2-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b7c2-209">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5b7c2-211">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5b7c2-213">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5b7c2-215">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5b7c2-217">а.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-217">a.</span></span> <span data-ttu-id="5b7c2-218">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b7c2-219">b.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-219">b.</span></span> <span data-ttu-id="5b7c2-220">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5b7c2-221">c.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-221">c.</span></span> <span data-ttu-id="5b7c2-222">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5b7c2-223">г)</span><span class="sxs-lookup"><span data-stu-id="5b7c2-223">d.</span></span> <span data-ttu-id="5b7c2-224">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="5b7c2-225">Создание тестового пользователя Litmos</span><span class="sxs-lookup"><span data-stu-id="5b7c2-225">Create a Litmos test user</span></span>

<span data-ttu-id="5b7c2-226">Цель этого раздела — создать пользователя с именем Britta Simon в Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="5b7c2-227">Приложение Litmos поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="5b7c2-228">Это значит, что учетная запись пользователя при необходимости создается автоматически во время попытки доступа к приложению с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="5b7c2-229">**Чтобы создать пользователя с именем Britta Simon в Litmos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5b7c2-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5b7c2-230">В другом окне браузера войдите на корпоративный сайт Litmos в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="5b7c2-231">В области навигации слева щелкните **Accounts**(Учетные записи).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Раздел "Accounts" (Учетные записи) на стороне приложения][22] 

3. <span data-ttu-id="5b7c2-233">Щелкните вкладку **Integrations** (Интеграции).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-233">Click the **Integrations** tab.</span></span>
   
    ![Вкладка "Integrations" (Интеграция)][23] 

4. <span data-ttu-id="5b7c2-235">На вкладке **Integrations** (Интеграции) прокрутите страницу вниз до раздела **3rd Party Integrations** (Интеграции сторонних поставщиков), а затем откройте вкладку **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="5b7c2-237">Установите флажок **Autogenerate Users** (Автоматически создавать пользователей).</span><span class="sxs-lookup"><span data-stu-id="5b7c2-237">Select **Autogenerate Users**</span></span>
   
    ![Автоматическое создание пользователей][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b7c2-239">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b7c2-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b7c2-240">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="5b7c2-242">**Чтобы назначить пользователя Britta Simon в Litmos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5b7c2-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="5b7c2-243">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5b7c2-245">В списке приложений выберите **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-245">In the applications list, select **Litmos**.</span></span>

    ![Ссылка на Litmos в списке "Приложения"](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="5b7c2-247">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="5b7c2-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-249">Click **Add** button.</span></span> <span data-ttu-id="5b7c2-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="5b7c2-252">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b7c2-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b7c2-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b7c2-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5b7c2-255">Test single sign-on</span></span>

<span data-ttu-id="5b7c2-256">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="5b7c2-257">Щелкнув элемент Litmos на панели доступа, вы автоматически войдете в приложение Litmos.</span><span class="sxs-lookup"><span data-stu-id="5b7c2-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b7c2-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5b7c2-258">Additional resources</span></span>

* [<span data-ttu-id="5b7c2-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b7c2-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b7c2-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b7c2-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

