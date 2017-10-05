---
title: "Учебник. Интеграция Azure Active Directory с DigiCert | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="e85e7-103">Учебник. Интеграция Azure Active Directory с DigiCert</span><span class="sxs-lookup"><span data-stu-id="e85e7-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="e85e7-104">В этом учебнике описано, как интегрировать DigiCert с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e85e7-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e85e7-105">Интеграция Azure AD с приложением DigiCert обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e85e7-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e85e7-106">С помощью Azure AD вы можете контролировать доступ к DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="e85e7-107">Вы можете включить автоматический вход пользователей в DigiCert (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e85e7-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e85e7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e85e7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e85e7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e85e7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e85e7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e85e7-110">Prerequisites</span></span>

<span data-ttu-id="e85e7-111">Чтобы настроить интеграцию Azure AD с DigiCert, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e85e7-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="e85e7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e85e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e85e7-113">подписка с поддержкой единого входа DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e85e7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e85e7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e85e7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e85e7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e85e7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e85e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e85e7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e85e7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e85e7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e85e7-118">Scenario description</span></span>
<span data-ttu-id="e85e7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e85e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e85e7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e85e7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e85e7-121">Добавление DigiCert из галереи</span><span class="sxs-lookup"><span data-stu-id="e85e7-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="e85e7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="e85e7-123">Добавление DigiCert из галереи</span><span class="sxs-lookup"><span data-stu-id="e85e7-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="e85e7-124">Чтобы настроить интеграцию DigiCert с Azure AD, необходимо добавить DigiCert из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e85e7-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e85e7-125">**Чтобы добавить DigiCert из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e85e7-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e85e7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e85e7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e85e7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e85e7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e85e7-133">В поле поиска введите **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-133">In the search box, type **DigiCert**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="e85e7-135">На панели результатов выберите **DigiCert** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e85e7-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e85e7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e85e7-138">В этом разделе описана настройка и проверка единого входа Azure AD в DigiCert с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e85e7-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e85e7-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в DigiCert соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e85e7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="e85e7-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="e85e7-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e85e7-142">Чтобы настроить и проверить единый вход Azure AD в DigiCert, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="e85e7-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e85e7-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e85e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e85e7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e85e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e85e7-145">**[Создание тестового пользователя DigiCert](#creating-a-digicert-test-user)** требуется для создания пользователя Britta Simon в DigiCert, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e85e7-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e85e7-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e85e7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e85e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e85e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e85e7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e85e7-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="e85e7-150">**Чтобы настроить единый вход Azure AD в DigiCert, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e85e7-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="e85e7-151">На портале Azure на странице интеграции с приложением **DigiCert** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e85e7-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e85e7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="e85e7-155">В разделе **Домен и URL-адреса единого входа в DigiCert** не нужно выполнять никаких действий, поскольку приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="e85e7-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="e85e7-157">Для приложения DigiCert требуется утверждение SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="e85e7-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e85e7-158">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e85e7-158">Configure the following claims for this application.</span></span> <span data-ttu-id="e85e7-159">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="e85e7-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e85e7-160">На следующем снимке экрана приведен пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e85e7-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="e85e7-162">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e85e7-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="e85e7-163">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="e85e7-163">Attribute Name</span></span> | <span data-ttu-id="e85e7-164">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="e85e7-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="e85e7-165">company</span><span class="sxs-lookup"><span data-stu-id="e85e7-165">company</span></span> | <span data-ttu-id="e85e7-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="e85e7-166">< companycode ></span></span> |
    | <span data-ttu-id="e85e7-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="e85e7-167">digicertrole</span></span> | <span data-ttu-id="e85e7-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="e85e7-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="e85e7-169">Значение атрибута **company** приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="e85e7-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="e85e7-170">Введите вместо этого значения фактический код компании.</span><span class="sxs-lookup"><span data-stu-id="e85e7-170">Update this value with actual company code.</span></span> <span data-ttu-id="e85e7-171">Чтобы получить значение атрибута **company**, обратитесь в [службу поддержки DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="e85e7-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="e85e7-172">а.</span><span class="sxs-lookup"><span data-stu-id="e85e7-172">a.</span></span> <span data-ttu-id="e85e7-173">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e85e7-176">b.</span><span class="sxs-lookup"><span data-stu-id="e85e7-176">b.</span></span> <span data-ttu-id="e85e7-177">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="e85e7-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="e85e7-178">c.</span><span class="sxs-lookup"><span data-stu-id="e85e7-178">c.</span></span> <span data-ttu-id="e85e7-179">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="e85e7-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e85e7-180">г)</span><span class="sxs-lookup"><span data-stu-id="e85e7-180">d.</span></span> <span data-ttu-id="e85e7-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="e85e7-182">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e85e7-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="e85e7-184">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e85e7-184">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e85e7-186">Чтобы настроить единый вход на стороне **DigiCert**, отправьте скачанный **XML-файл метаданных** в [службу поддержки DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="e85e7-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="e85e7-187">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="e85e7-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e85e7-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e85e7-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e85e7-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e85e7-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e85e7-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e85e7-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e85e7-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85e7-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="e85e7-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e85e7-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e85e7-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e85e7-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e85e7-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e85e7-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e85e7-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e85e7-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e85e7-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e85e7-203">а.</span><span class="sxs-lookup"><span data-stu-id="e85e7-203">a.</span></span> <span data-ttu-id="e85e7-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e85e7-205">b.</span><span class="sxs-lookup"><span data-stu-id="e85e7-205">b.</span></span> <span data-ttu-id="e85e7-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e85e7-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e85e7-207">c.</span><span class="sxs-lookup"><span data-stu-id="e85e7-207">c.</span></span> <span data-ttu-id="e85e7-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e85e7-209">d.</span><span class="sxs-lookup"><span data-stu-id="e85e7-209">d.</span></span> <span data-ttu-id="e85e7-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="e85e7-211">Создание тестового пользователя DigiCert</span><span class="sxs-lookup"><span data-stu-id="e85e7-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="e85e7-212">В этом разделе описано, как создать пользователя Britta Simon в приложении DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="e85e7-213">Обратитесь в [службу поддержки DigiCert](mailto:support@digicert.com), чтобы добавить пользователей в DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e85e7-214">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85e7-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e85e7-215">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e85e7-217">**Чтобы назначить пользователя Britta Simon в DigiCert, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e85e7-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="e85e7-218">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e85e7-220">В списке приложений выберите **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-220">In the applications list, select **DigiCert**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="e85e7-222">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e85e7-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-224">Click **Add** button.</span></span> <span data-ttu-id="e85e7-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e85e7-227">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e85e7-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e85e7-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e85e7-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e85e7-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e85e7-230">Testing single sign-on</span></span>

<span data-ttu-id="e85e7-231">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e85e7-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e85e7-232">Щелкнув элемент DigiCert на панели доступа, вы автоматически войдете в приложение DigiCert.</span><span class="sxs-lookup"><span data-stu-id="e85e7-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="e85e7-233">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e85e7-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e85e7-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e85e7-234">Additional resources</span></span>

* [<span data-ttu-id="e85e7-235">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e85e7-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e85e7-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e85e7-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

