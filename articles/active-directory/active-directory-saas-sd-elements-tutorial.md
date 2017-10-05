---
title: "Руководство по интеграции Azure Active Directory с SD Elements | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и SD Elements."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="07dde-103">Учебник. Интеграция Azure Active Directory с SD Elements</span><span class="sxs-lookup"><span data-stu-id="07dde-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="07dde-104">В этом руководстве описано, как интегрировать SD Elements с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07dde-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07dde-105">Интеграция Azure AD с приложением SD Elements обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="07dde-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07dde-106">С помощью Azure AD вы можете контролировать доступ к приложению SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="07dde-107">Вы можете включить автоматический вход пользователей в SD Elements (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07dde-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07dde-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="07dde-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07dde-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07dde-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07dde-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="07dde-110">Prerequisites</span></span>

<span data-ttu-id="07dde-111">Чтобы настроить интеграцию Azure AD с SD Elements, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="07dde-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="07dde-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="07dde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07dde-113">подписка SD Elements с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="07dde-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07dde-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="07dde-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07dde-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="07dde-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07dde-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="07dde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07dde-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07dde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07dde-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="07dde-118">Scenario description</span></span>
<span data-ttu-id="07dde-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="07dde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07dde-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="07dde-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07dde-121">Добавление SD Elements из коллекции.</span><span class="sxs-lookup"><span data-stu-id="07dde-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="07dde-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07dde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="07dde-123">Добавление SD Elements из коллекции.</span><span class="sxs-lookup"><span data-stu-id="07dde-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="07dde-124">Чтобы настроить интеграцию SD Elements с Azure AD, необходимо добавить SD Elements из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="07dde-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07dde-125">**Чтобы добавить SD Elements из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="07dde-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07dde-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07dde-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07dde-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="07dde-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07dde-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="07dde-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="07dde-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="07dde-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="07dde-133">В поле поиска введите **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="07dde-133">In the search box, type **SD Elements**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="07dde-135">На панели результатов выберите **SD Elements** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="07dde-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07dde-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07dde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07dde-138">В этом разделе описана настройка и проверка единого входа Azure AD в SD Elements с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07dde-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07dde-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в SD Elements соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07dde-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="07dde-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="07dde-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07dde-142">Чтобы настроить и проверить единый вход Azure AD в SD Elements, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="07dde-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07dde-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="07dde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07dde-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07dde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07dde-145">**[Создание тестового пользователя SD Elements](#creating-a-sd-elements-test-user)** требуется для того, чтобы в SD Elements существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07dde-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07dde-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07dde-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07dde-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="07dde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07dde-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07dde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07dde-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="07dde-150">**Чтобы настроить единый вход Azure AD в SD Elements, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="07dde-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="07dde-151">На портале Azure на странице интеграции с приложением **SD Elements** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="07dde-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="07dde-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="07dde-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="07dde-155">В разделе **Домены и URL-адреса приложения SD Elements** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="07dde-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="07dde-157">а.</span><span class="sxs-lookup"><span data-stu-id="07dde-157">a.</span></span> <span data-ttu-id="07dde-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="07dde-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="07dde-159">b.</span><span class="sxs-lookup"><span data-stu-id="07dde-159">b.</span></span> <span data-ttu-id="07dde-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<tenantname>.sdelements.com/sso/saml2/acs/`.</span><span class="sxs-lookup"><span data-stu-id="07dde-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07dde-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="07dde-161">These values are not real.</span></span> <span data-ttu-id="07dde-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="07dde-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="07dde-163">Чтобы получить эти значения, обратитесь к [группе поддержки SD Elements](mailto:support@sdelements.com).</span><span class="sxs-lookup"><span data-stu-id="07dde-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="07dde-164">SD Elements ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="07dde-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="07dde-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="07dde-165">Configure the following claims for this application.</span></span> <span data-ttu-id="07dde-166">Управлять значениями этих атрибутов можно на вкладке **Атрибуты пользователя** приложения.</span><span class="sxs-lookup"><span data-stu-id="07dde-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="07dde-167">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="07dde-167">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="07dde-169">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07dde-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="07dde-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="07dde-170">Attribute Name</span></span> | <span data-ttu-id="07dde-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="07dde-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="07dde-172">email</span><span class="sxs-lookup"><span data-stu-id="07dde-172">email</span></span> |<span data-ttu-id="07dde-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="07dde-173">user.mail</span></span> |
    | <span data-ttu-id="07dde-174">firstname</span><span class="sxs-lookup"><span data-stu-id="07dde-174">firstname</span></span> |<span data-ttu-id="07dde-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="07dde-175">user.givenname</span></span> |
    | <span data-ttu-id="07dde-176">lastname</span><span class="sxs-lookup"><span data-stu-id="07dde-176">lastname</span></span> |<span data-ttu-id="07dde-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="07dde-177">user.surname</span></span> |

    <span data-ttu-id="07dde-178">а.</span><span class="sxs-lookup"><span data-stu-id="07dde-178">a.</span></span> <span data-ttu-id="07dde-179">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="07dde-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="07dde-182">b.</span><span class="sxs-lookup"><span data-stu-id="07dde-182">b.</span></span> <span data-ttu-id="07dde-183">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="07dde-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="07dde-184">c.</span><span class="sxs-lookup"><span data-stu-id="07dde-184">c.</span></span> <span data-ttu-id="07dde-185">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="07dde-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="07dde-186">г)</span><span class="sxs-lookup"><span data-stu-id="07dde-186">d.</span></span> <span data-ttu-id="07dde-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="07dde-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="07dde-188">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="07dde-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="07dde-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="07dde-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="07dde-192">В разделе **Конфигурация SD Elements** щелкните **Настроить SD Elements**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="07dde-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07dde-193">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="07dde-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="07dde-195">Чтобы включить единый вход, обратитесь в [службу поддержки SD Elements](mailto:support@sdelements.com) и предоставьте загруженный файл сертификата.</span><span class="sxs-lookup"><span data-stu-id="07dde-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="07dde-196">В другом окне браузера войдите в клиент SD Elements в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="07dde-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="07dde-197">В верхнем меню выберите **System** (Система) и щелкните **Single Sign-on** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="07dde-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="07dde-199">В диалоговом окне **Параметры единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07dde-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="07dde-201">а.</span><span class="sxs-lookup"><span data-stu-id="07dde-201">a.</span></span> <span data-ttu-id="07dde-202">Для параметра **SSO Type** (Тип SSO) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="07dde-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="07dde-203">b.</span><span class="sxs-lookup"><span data-stu-id="07dde-203">b.</span></span> <span data-ttu-id="07dde-204">В текстовое поле **Identity Provider Entity ID** (Идентификатор сущности поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="07dde-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="07dde-205">c.</span><span class="sxs-lookup"><span data-stu-id="07dde-205">c.</span></span> <span data-ttu-id="07dde-206">В текстовое поле **Identity Provider Single Sign-On Service** (Служба единого входа поставщика удостоверений) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="07dde-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="07dde-207">г)</span><span class="sxs-lookup"><span data-stu-id="07dde-207">d.</span></span> <span data-ttu-id="07dde-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="07dde-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="07dde-209">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="07dde-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07dde-210">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="07dde-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07dde-211">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="07dde-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07dde-212">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="07dde-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="07dde-213">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07dde-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="07dde-215">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="07dde-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07dde-216">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07dde-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07dde-218">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="07dde-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07dde-220">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="07dde-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07dde-222">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07dde-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07dde-224">а.</span><span class="sxs-lookup"><span data-stu-id="07dde-224">a.</span></span> <span data-ttu-id="07dde-225">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07dde-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07dde-226">b.</span><span class="sxs-lookup"><span data-stu-id="07dde-226">b.</span></span> <span data-ttu-id="07dde-227">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="07dde-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07dde-228">c.</span><span class="sxs-lookup"><span data-stu-id="07dde-228">c.</span></span> <span data-ttu-id="07dde-229">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="07dde-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07dde-230">d.</span><span class="sxs-lookup"><span data-stu-id="07dde-230">d.</span></span> <span data-ttu-id="07dde-231">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="07dde-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="07dde-232">Создание тестового пользователя SD Elements</span><span class="sxs-lookup"><span data-stu-id="07dde-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="07dde-233">Цель этого раздела — создать в приложении SD Elements пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07dde-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="07dde-234">Пользователи SD Elements создаются вручную.</span><span class="sxs-lookup"><span data-stu-id="07dde-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="07dde-235">**Чтобы создать пользователя с именем Britta Simon в SD Elements, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="07dde-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="07dde-236">Откройте браузер и войдите на корпоративный сайт SD Elements с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="07dde-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="07dde-237">На панели инструментов вверху щелкните **User Management** (Управление пользователями), а затем щелкните **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="07dde-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="07dde-239">Нажмите кнопку **Add New User**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="07dde-239">Click **Add New User**.</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="07dde-241">В диалоговом окне **Add New User** (Добавление нового пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07dde-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Создание тестового пользователя SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="07dde-243">а.</span><span class="sxs-lookup"><span data-stu-id="07dde-243">a.</span></span> <span data-ttu-id="07dde-244">В текстовое поле **E-mail** (Электронная почта) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="07dde-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="07dde-245">b.</span><span class="sxs-lookup"><span data-stu-id="07dde-245">b.</span></span> <span data-ttu-id="07dde-246">В текстовое поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="07dde-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="07dde-247">c.</span><span class="sxs-lookup"><span data-stu-id="07dde-247">c.</span></span> <span data-ttu-id="07dde-248">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="07dde-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="07dde-249">г)</span><span class="sxs-lookup"><span data-stu-id="07dde-249">d.</span></span> <span data-ttu-id="07dde-250">Для параметра **Role** (Роль) выберите значение **User** (Пользователь).</span><span class="sxs-lookup"><span data-stu-id="07dde-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="07dde-251">д.</span><span class="sxs-lookup"><span data-stu-id="07dde-251">e.</span></span> <span data-ttu-id="07dde-252">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="07dde-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07dde-253">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="07dde-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07dde-254">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="07dde-256">**Чтобы назначить пользователя Britta Simon в SD Elements, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="07dde-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="07dde-257">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="07dde-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="07dde-259">В списке приложений выберите **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="07dde-259">In the applications list, select **SD Elements**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="07dde-261">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="07dde-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="07dde-263">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="07dde-263">Click **Add** button.</span></span> <span data-ttu-id="07dde-264">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="07dde-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="07dde-266">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="07dde-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07dde-267">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="07dde-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07dde-268">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="07dde-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07dde-269">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="07dde-269">Testing single sign-on</span></span>

<span data-ttu-id="07dde-270">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="07dde-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="07dde-271">Щелкнув элемент SD Elements на панели доступа, вы автоматически войдете в приложение SD Elements.</span><span class="sxs-lookup"><span data-stu-id="07dde-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07dde-272">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="07dde-272">Additional resources</span></span>

* [<span data-ttu-id="07dde-273">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07dde-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07dde-274">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07dde-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

