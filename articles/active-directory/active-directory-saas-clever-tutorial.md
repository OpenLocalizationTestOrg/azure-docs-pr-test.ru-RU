---
title: "Учебник. Интеграция Azure Active Directory с Clever | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="8fa8f-103">Руководство. Интеграция Azure Active Directory с Clever</span><span class="sxs-lookup"><span data-stu-id="8fa8f-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="8fa8f-104">В этом учебнике описано, как интегрировать Clever с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8fa8f-105">Интеграция Azure AD с приложением Clever обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8fa8f-106">С помощью Azure AD вы можете контролировать доступ к Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="8fa8f-107">Вы можете включить автоматический вход пользователей в Clever (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8fa8f-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8fa8f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fa8f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8fa8f-110">Prerequisites</span></span>

<span data-ttu-id="8fa8f-111">Чтобы настроить интеграцию Azure AD с Clever, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8fa8f-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="8fa8f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8fa8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8fa8f-113">подписка Clever с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8fa8f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8fa8f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8fa8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8fa8f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8fa8f-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8fa8f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8fa8f-118">Scenario description</span></span>
<span data-ttu-id="8fa8f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8fa8f-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8fa8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8fa8f-121">Добавление Clever из коллекции</span><span class="sxs-lookup"><span data-stu-id="8fa8f-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="8fa8f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="8fa8f-123">Добавление Clever из коллекции</span><span class="sxs-lookup"><span data-stu-id="8fa8f-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="8fa8f-124">Чтобы настроить интеграцию Clever с Azure AD, необходимо добавить Clever из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8fa8f-125">**Чтобы добавить Clever из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8fa8f-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8fa8f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="8fa8f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8fa8f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="8fa8f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="8fa8f-133">В поле поиска введите **Clever**, выберите **Clever** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever в списке результатов](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8fa8f-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa8f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8fa8f-136">В этом разделе описана настройка и проверка единого входа Azure AD в Clever с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8fa8f-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Clever соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="8fa8f-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="8fa8f-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8fa8f-140">Чтобы настроить и проверить единый вход Azure AD в Clever, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8fa8f-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8fa8f-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8fa8f-143">**[Создание тестового пользователя Clever](#create-a-clever-test-user)** требуется для того, чтобы в Clever существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8fa8f-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8fa8f-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8fa8f-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa8f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8fa8f-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="8fa8f-148">**Чтобы настроить единый вход Azure AD в Clever, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8fa8f-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="8fa8f-149">На портале Azure на странице интеграции с приложением **Clever** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="8fa8f-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="8fa8f-153">В разделе **Домены и URL-адреса приложения Clever** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8fa8f-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="8fa8f-155">а.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-155">a.</span></span> <span data-ttu-id="8fa8f-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8fa8f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="8fa8f-157">b.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-157">b.</span></span> <span data-ttu-id="8fa8f-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8fa8f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8fa8f-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-159">These values are not real.</span></span> <span data-ttu-id="8fa8f-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8fa8f-161">Чтобы получить их, обратитесь в [службу поддержки клиентов Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="8fa8f-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="8fa8f-164">Приложение Clever ожидает проверочные утверждения SAML в определенном формате, и поэтому вам нужно добавить в конфигурацию **атрибутов токена SAML** сопоставления настраиваемых атрибутов.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="8fa8f-165">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-165">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="8fa8f-167">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8fa8f-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8fa8f-168">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="8fa8f-168">Attribute Name</span></span>  | <span data-ttu-id="8fa8f-169">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="8fa8f-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="8fa8f-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="8fa8f-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="8fa8f-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8fa8f-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="8fa8f-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="8fa8f-172">Firstname</span></span>  | <span data-ttu-id="8fa8f-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8fa8f-173">user.givenname</span></span> |
    | <span data-ttu-id="8fa8f-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="8fa8f-174">Lastname</span></span>  | <span data-ttu-id="8fa8f-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8fa8f-175">user.surname</span></span> |    

    <span data-ttu-id="8fa8f-176">а.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-176">a.</span></span> <span data-ttu-id="8fa8f-177">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8fa8f-180">b.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-180">b.</span></span> <span data-ttu-id="8fa8f-181">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="8fa8f-182">c.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-182">c.</span></span> <span data-ttu-id="8fa8f-183">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="8fa8f-184">г)</span><span class="sxs-lookup"><span data-stu-id="8fa8f-184">d.</span></span> <span data-ttu-id="8fa8f-185">Оставьте пустым текстовое поле **Пространство имен**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="8fa8f-186">d.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-186">d.</span></span> <span data-ttu-id="8fa8f-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="8fa8f-188">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8fa8f-188">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8fa8f-190">Для создания URL-адреса **метаданных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="8fa8f-191">а.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-191">a.</span></span> <span data-ttu-id="8fa8f-192">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-192">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="8fa8f-194">b.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-194">b.</span></span> <span data-ttu-id="8fa8f-195">Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="8fa8f-197">c.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-197">c.</span></span> <span data-ttu-id="8fa8f-198">Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="8fa8f-200">d.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-200">d.</span></span> <span data-ttu-id="8fa8f-201">Теперь перейдите на страницу свойств **Clever** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="8fa8f-203">д.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-203">e.</span></span> <span data-ttu-id="8fa8f-204">Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="8fa8f-205">В другом окне веб-браузера войдите на корпоративный веб-сайт Clever в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="8fa8f-206">На панели инструментов выберите **Мгновенный вход**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="8fa8f-207">![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798984.png "Мгновенный вход")</span><span class="sxs-lookup"><span data-stu-id="8fa8f-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="8fa8f-208">На странице **Мгновенный вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="8fa8f-209">![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798985.png "Мгновенный вход")</span><span class="sxs-lookup"><span data-stu-id="8fa8f-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="8fa8f-210">а.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-210">a.</span></span> <span data-ttu-id="8fa8f-211">Введите **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="8fa8f-212">**URL-адрес входа** является настраиваемым значением.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="8fa8f-213">Чтобы получить это значение, обратитесь к [группе поддержки клиентов Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="8fa8f-214">b.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-214">b.</span></span> <span data-ttu-id="8fa8f-215">Для параметра **Identity System** (Система идентификации) выберите значение **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="8fa8f-216">c.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-216">c.</span></span> <span data-ttu-id="8fa8f-217">Введите **URL-адрес метаданных** в текстовое поле **Metadata URL** (URL-адрес метаданных).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="8fa8f-218">d.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-218">d.</span></span> <span data-ttu-id="8fa8f-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8fa8f-220">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8fa8f-221">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8fa8f-222">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8fa8f-223">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa8f-223">Create an Azure AD test user</span></span>

<span data-ttu-id="8fa8f-224">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="8fa8f-226">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8fa8f-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8fa8f-227">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8fa8f-229">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8fa8f-231">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8fa8f-233">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8fa8f-235">а.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-235">a.</span></span> <span data-ttu-id="8fa8f-236">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8fa8f-237">b.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-237">b.</span></span> <span data-ttu-id="8fa8f-238">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8fa8f-239">c.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-239">c.</span></span> <span data-ttu-id="8fa8f-240">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8fa8f-241">г)</span><span class="sxs-lookup"><span data-stu-id="8fa8f-241">d.</span></span> <span data-ttu-id="8fa8f-242">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="8fa8f-243">Создание тестового пользователя Clever</span><span class="sxs-lookup"><span data-stu-id="8fa8f-243">Create a Clever test user</span></span>

<span data-ttu-id="8fa8f-244">Чтобы пользователи Azure AD могли выполнить вход в Clever, они должны быть подготовлены для Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="8fa8f-245">Обратитесь в [службу поддержки Clever](https://clever.com/about/contact/), чтобы добавить пользователей для платформы Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="8fa8f-246">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="8fa8f-247">Вы можете использовать любые другие инструменты для создания учетной записи пользователя Clever или API, предоставляемые Clever для подготовки учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8fa8f-248">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8fa8f-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="8fa8f-249">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="8fa8f-251">**Чтобы назначить пользователя Britta Simon в Clever, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8fa8f-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="8fa8f-252">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8fa8f-254">В списке приложений выберите **Clever**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-254">In the applications list, select **Clever**.</span></span>

    ![Ссылка на Clever в списке "Приложения"](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="8fa8f-256">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="8fa8f-258">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-258">Click **Add** button.</span></span> <span data-ttu-id="8fa8f-259">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="8fa8f-261">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8fa8f-262">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8fa8f-263">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8fa8f-264">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8fa8f-264">Test single sign-on</span></span>

<span data-ttu-id="8fa8f-265">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8fa8f-266">Щелкнув плитку Clever на панели доступа, вы автоматически войдете в приложение Clever.</span><span class="sxs-lookup"><span data-stu-id="8fa8f-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="8fa8f-267">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8fa8f-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8fa8f-268">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8fa8f-268">Additional resources</span></span>

* [<span data-ttu-id="8fa8f-269">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fa8f-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8fa8f-270">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8fa8f-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

