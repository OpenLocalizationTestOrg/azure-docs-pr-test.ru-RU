---
title: "Учебник. Интеграция Azure Active Directory с CloudPassage | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="5c3d3-103">Учебник. Интеграция Azure Active Directory с CloudPassage</span><span class="sxs-lookup"><span data-stu-id="5c3d3-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="5c3d3-104">В этом учебнике описано, как интегрировать приложение CloudPassage с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c3d3-105">Интеграция приложения CloudPassage с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c3d3-106">С помощью Azure AD вы можете контролировать доступ к CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="5c3d3-107">Вы можете включить автоматический вход пользователей в CloudPassage (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c3d3-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c3d3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c3d3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c3d3-110">Prerequisites</span></span>

<span data-ttu-id="5c3d3-111">Чтобы настроить интеграцию Azure AD с CloudPassage, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="5c3d3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5c3d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c3d3-113">подписка CloudPassage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c3d3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c3d3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c3d3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c3d3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c3d3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5c3d3-118">Scenario description</span></span>
<span data-ttu-id="5c3d3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c3d3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c3d3-121">Добавление CloudPassage из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c3d3-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="5c3d3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="5c3d3-123">Добавление CloudPassage из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c3d3-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="5c3d3-124">Чтобы настроить интеграцию CloudPassage с Azure AD, вам потребуется добавить CloudPassage из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c3d3-125">**Чтобы добавить CloudPassage из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c3d3-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3d3-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c3d3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c3d3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5c3d3-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5c3d3-133">В поле поиска введите **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-133">In the search box, type **CloudPassage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="5c3d3-135">На панели результатов выберите **CloudPassage** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c3d3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c3d3-138">В этом разделе описана настройка и проверка единого входа Azure AD в CloudPassage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c3d3-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в CloudPassage соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="5c3d3-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="5c3d3-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c3d3-142">Чтобы настроить и проверить единый вход Azure AD в CloudPassage, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c3d3-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c3d3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c3d3-145">**[Создание тестового пользователя CloudPassage](#creating-a-cloudpassage-test-user)** требуется для создания соответствующего пользователя Britta Simon в CloudPassage, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c3d3-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c3d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c3d3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c3d3-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="5c3d3-150">**Чтобы настроить единый вход Azure AD в CloudPassage, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c3d3-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3d3-151">На портале Azure на странице интеграции с приложением **CloudPassage** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5c3d3-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="5c3d3-155">В разделе **Домен и URL-адреса приложения CloudPassage** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="5c3d3-157">а.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-157">a.</span></span> <span data-ttu-id="5c3d3-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="5c3d3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="5c3d3-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-159">b.</span></span> <span data-ttu-id="5c3d3-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="5c3d3-161">Значение этого атрибута можно получить, щелкнув **SSO Setup documentation** (Документация по настройке единого входа) в разделе **Single Sign-on Settings** на портале CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="5c3d3-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-163">These values are not real.</span></span> <span data-ttu-id="5c3d3-164">Измените их на фактические значения URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5c3d3-165">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов CloudPassage](https://www.cloudpassage.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="5c3d3-166">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="5c3d3-168">Приложение CloudPassage ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5c3d3-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-169">The following screenshot shows an example for this.</span></span>
   
   ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="5c3d3-171">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="5c3d3-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="5c3d3-172">Attribute Name</span></span> | <span data-ttu-id="5c3d3-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="5c3d3-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5c3d3-174">firstname</span><span class="sxs-lookup"><span data-stu-id="5c3d3-174">firstname</span></span> |<span data-ttu-id="5c3d3-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="5c3d3-175">user.givenname</span></span> |
    | <span data-ttu-id="5c3d3-176">lastname</span><span class="sxs-lookup"><span data-stu-id="5c3d3-176">lastname</span></span> |<span data-ttu-id="5c3d3-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="5c3d3-177">user.surname</span></span> |
    | <span data-ttu-id="5c3d3-178">email</span><span class="sxs-lookup"><span data-stu-id="5c3d3-178">email</span></span> |<span data-ttu-id="5c3d3-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="5c3d3-179">user.mail</span></span> |
    
    <span data-ttu-id="5c3d3-180">а.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-180">a.</span></span> <span data-ttu-id="5c3d3-181">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5c3d3-184">b.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-184">b.</span></span> <span data-ttu-id="5c3d3-185">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5c3d3-186">c.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-186">c.</span></span> <span data-ttu-id="5c3d3-187">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5c3d3-188">г)</span><span class="sxs-lookup"><span data-stu-id="5c3d3-188">d.</span></span> <span data-ttu-id="5c3d3-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-189">Click **Ok**.</span></span>

7. <span data-ttu-id="5c3d3-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5c3d3-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="5c3d3-192">В разделе **Настройка CloudPassage** щелкните **Настроить Clarizen**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c3d3-193">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="5c3d3-195">В другом окне браузера войдите на сайт CloudPassage компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="5c3d3-196">В верхнем меню щелкните **Параметры**, а затем выберите **Администрирование сайта**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Настройка единого входа][12]

11. <span data-ttu-id="5c3d3-198">Выберите вкладку **Параметры проверки подлинности** .</span><span class="sxs-lookup"><span data-stu-id="5c3d3-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Настройка единого входа][13]

12. <span data-ttu-id="5c3d3-200">В разделе **Параметры единого входа** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5c3d3-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Настройка единого входа][14]

    <span data-ttu-id="5c3d3-202">а.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-202">a.</span></span> <span data-ttu-id="5c3d3-203">Установите флажок **Enable Single sign-on(SSO)(SSO Setup Documentation)** (Включить единый вход (SSO) (Документация по настройке единого входа)).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="5c3d3-204">b.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-204">b.</span></span> <span data-ttu-id="5c3d3-205">Вставьте **идентификатор сущности SAML** в текстовое поле **URL-адрес издателя SAML**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="5c3d3-206">c.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-206">c.</span></span> <span data-ttu-id="5c3d3-207">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **URL-адрес конечной точки SAML**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="5c3d3-208">г)</span><span class="sxs-lookup"><span data-stu-id="5c3d3-208">d.</span></span> <span data-ttu-id="5c3d3-209">Вставьте **URL-адрес выхода** в текстовое поле **Целевая страница выхода**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="5c3d3-210">д.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-210">e.</span></span> <span data-ttu-id="5c3d3-211">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="5c3d3-212">Е.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-212">f.</span></span> <span data-ttu-id="5c3d3-213">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5c3d3-214">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c3d3-215">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c3d3-216">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c3d3-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3d3-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c3d3-218">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5c3d3-220">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c3d3-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3d3-221">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c3d3-223">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c3d3-225">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c3d3-227">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c3d3-229">а.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-229">a.</span></span> <span data-ttu-id="5c3d3-230">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c3d3-231">b.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-231">b.</span></span> <span data-ttu-id="5c3d3-232">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c3d3-233">c.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-233">c.</span></span> <span data-ttu-id="5c3d3-234">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c3d3-235">d.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-235">d.</span></span> <span data-ttu-id="5c3d3-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="5c3d3-237">Создание тестового пользователя CloudPassage</span><span class="sxs-lookup"><span data-stu-id="5c3d3-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="5c3d3-238">Цель этого раздела — создать пользователя с именем Britta Simon в CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="5c3d3-239">**Чтобы создать пользователя с именем Britta Simon в CloudPassage, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c3d3-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3d3-240">Выполните вход на сайт **CloudPassage** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="5c3d3-241">На панели инструментов в верхней части экрана щелкните **Settings** (Параметры), а затем выберите **Site Administration** (Администрирование сайта).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Создание тестового пользователя CloudPassage][22] 

3. <span data-ttu-id="5c3d3-243">Откройте вкладку **Пользователи**, а затем щелкните **Добавить нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Создание тестового пользователя CloudPassage][23]

4. <span data-ttu-id="5c3d3-245">В разделе **Добавить нового пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Создание тестового пользователя CloudPassage][24]
    
    <span data-ttu-id="5c3d3-247">а.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-247">a.</span></span> <span data-ttu-id="5c3d3-248">В текстовом поле **Имя** введите Britta.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="5c3d3-249">b.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-249">b.</span></span> <span data-ttu-id="5c3d3-250">В текстовом поле **Фамилия** введите Simon.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="5c3d3-251">c.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-251">c.</span></span> <span data-ttu-id="5c3d3-252">В текстовых полях **Username** (Имя пользователя), **Email** (Электронная почта) и **Retype Email** (Введите адрес еще раз) укажите данные, соответствующие пользователю Britta в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="5c3d3-253">d.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-253">d.</span></span> <span data-ttu-id="5c3d3-254">Для параметра **Access Type** (Тип доступа) выберите **Enable Halo Portal Access** (Включить доступ к порталу Halo).</span><span class="sxs-lookup"><span data-stu-id="5c3d3-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="5c3d3-255">д.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-255">e.</span></span> <span data-ttu-id="5c3d3-256">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c3d3-257">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c3d3-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c3d3-258">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5c3d3-260">**Чтобы назначить Britta Simon в CloudPassage, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c3d3-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="5c3d3-261">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5c3d3-263">В списке приложений выберите **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-263">In the applications list, select **CloudPassage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="5c3d3-265">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5c3d3-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-267">Click **Add** button.</span></span> <span data-ttu-id="5c3d3-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5c3d3-270">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c3d3-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c3d3-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c3d3-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5c3d3-273">Testing single sign-on</span></span>

<span data-ttu-id="5c3d3-274">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5c3d3-275">Щелкнув элемент CloudPassage на панели доступа, вы автоматически войдете в приложение CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="5c3d3-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c3d3-276">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5c3d3-276">Additional resources</span></span>

* [<span data-ttu-id="5c3d3-277">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c3d3-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c3d3-278">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c3d3-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

