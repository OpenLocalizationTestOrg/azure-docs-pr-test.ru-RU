---
title: "Руководство по интеграции Azure Active Directory с BenefitHub | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="5c71a-103">Руководство по интеграции Azure Active Directory с BenefitHub</span><span class="sxs-lookup"><span data-stu-id="5c71a-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="5c71a-104">В этом руководстве описано, как интегрировать BenefitHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c71a-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c71a-105">Интеграция Azure AD с приложением BenefitHub обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5c71a-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c71a-106">С помощью Azure AD вы можете контролировать доступ к BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="5c71a-107">Вы можете включить автоматический вход пользователей в BenefitHub (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c71a-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c71a-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5c71a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c71a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c71a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c71a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c71a-110">Prerequisites</span></span>

<span data-ttu-id="5c71a-111">Чтобы настроить интеграцию Azure AD с BenefitHub, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5c71a-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="5c71a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5c71a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c71a-113">подписка BenefitHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c71a-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c71a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5c71a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c71a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5c71a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c71a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5c71a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c71a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c71a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c71a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5c71a-118">Scenario description</span></span>
<span data-ttu-id="5c71a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5c71a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c71a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5c71a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c71a-121">Добавление BenefitHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c71a-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="5c71a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c71a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="5c71a-123">Добавление BenefitHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c71a-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="5c71a-124">Чтобы настроить интеграцию BenefitHub с Azure AD, необходимо добавить BenefitHub из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c71a-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c71a-125">**Чтобы добавить BenefitHub из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="5c71a-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c71a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c71a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c71a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5c71a-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5c71a-133">В поле поиска введите **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-133">In the search box, type **BenefitHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="5c71a-135">На панели результатов выберите **BenefitHub** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="5c71a-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c71a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c71a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c71a-138">В этом разделе описана настройка и проверка единого входа Azure AD в BenefitHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c71a-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c71a-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BenefitHub соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c71a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="5c71a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="5c71a-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c71a-142">Чтобы настроить и проверить единый вход Azure AD в BenefitHub, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="5c71a-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c71a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5c71a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c71a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c71a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c71a-145">**[Создание тестового пользователя BenefitHub](#creating-a-benefithub-test-user)** нужно для того, чтобы в BenefitHub также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c71a-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c71a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c71a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c71a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5c71a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c71a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c71a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c71a-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="5c71a-150">**Чтобы настроить единый вход Azure AD в BenefitHub, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5c71a-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="5c71a-151">На портале Azure на странице интеграции с приложением **BenefitHub** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5c71a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c71a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="5c71a-155">В разделе **Домены и URL-адреса приложения BenefitHub** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5c71a-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="5c71a-157">а.</span><span class="sxs-lookup"><span data-stu-id="5c71a-157">a.</span></span> <span data-ttu-id="5c71a-158">В текстовом поле **Идентификатор** введите `urn:benefithub:passport`.</span><span class="sxs-lookup"><span data-stu-id="5c71a-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="5c71a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c71a-159">b.</span></span> <span data-ttu-id="5c71a-160">В текстовом поле **URL-адрес ответа** введите: `https://passport.benefithub.info/saml/post/ac`.</span><span class="sxs-lookup"><span data-stu-id="5c71a-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="5c71a-161">Приложение BenefitHub ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="5c71a-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5c71a-162">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5c71a-162">Configure the following claims for this application.</span></span> <span data-ttu-id="5c71a-163">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="5c71a-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="5c71a-165">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c71a-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5c71a-166">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="5c71a-166">Attribute Name</span></span> | <span data-ttu-id="5c71a-167">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="5c71a-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5c71a-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="5c71a-168">organizationid</span></span> | <span data-ttu-id="5c71a-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="5c71a-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="5c71a-170">Это значение атрибута приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="5c71a-170">This attribute value is not real.</span></span> <span data-ttu-id="5c71a-171">Введите вместо этого значения фактическое значение organizationid.</span><span class="sxs-lookup"><span data-stu-id="5c71a-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="5c71a-172">Обратитесь к [группе поддержки BenefitHub](https://www.benefithub.com/Home/ContactUs) для получения фактического значения organizationid.</span><span class="sxs-lookup"><span data-stu-id="5c71a-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="5c71a-173">а.</span><span class="sxs-lookup"><span data-stu-id="5c71a-173">a.</span></span> <span data-ttu-id="5c71a-174">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5c71a-177">b.</span><span class="sxs-lookup"><span data-stu-id="5c71a-177">b.</span></span> <span data-ttu-id="5c71a-178">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5c71a-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5c71a-179">c.</span><span class="sxs-lookup"><span data-stu-id="5c71a-179">c.</span></span> <span data-ttu-id="5c71a-180">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="5c71a-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5c71a-181">г)</span><span class="sxs-lookup"><span data-stu-id="5c71a-181">d.</span></span> <span data-ttu-id="5c71a-182">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c71a-183">Чтобы настроить утверждение SAML, обратитесь в [службу поддержки BenefitHub](https://www.benefithub.com/Home/ContactUs) и запросите значение атрибута уникального идентификатора для своего клиента.</span><span class="sxs-lookup"><span data-stu-id="5c71a-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="5c71a-184">Это значение необходимо для настройки пользовательского утверждения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5c71a-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="5c71a-185">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c71a-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="5c71a-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5c71a-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5c71a-189">Чтобы настроить единый вход на стороне **BenefitHub**, отправьте скачанный **XML-файл метаданных** [группе поддержки BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="5c71a-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="5c71a-190">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="5c71a-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5c71a-191">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5c71a-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c71a-192">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5c71a-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c71a-193">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5c71a-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c71a-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c71a-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c71a-195">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c71a-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5c71a-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c71a-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c71a-198">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c71a-200">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c71a-202">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c71a-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c71a-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c71a-206">а.</span><span class="sxs-lookup"><span data-stu-id="5c71a-206">a.</span></span> <span data-ttu-id="5c71a-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c71a-208">b.</span><span class="sxs-lookup"><span data-stu-id="5c71a-208">b.</span></span> <span data-ttu-id="5c71a-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c71a-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c71a-210">c.</span><span class="sxs-lookup"><span data-stu-id="5c71a-210">c.</span></span> <span data-ttu-id="5c71a-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c71a-212">d.</span><span class="sxs-lookup"><span data-stu-id="5c71a-212">d.</span></span> <span data-ttu-id="5c71a-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="5c71a-214">Создание тестового пользователя BenefitHub</span><span class="sxs-lookup"><span data-stu-id="5c71a-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="5c71a-215">В этом разделе описано, как создать пользователя Britta Simon в приложении BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="5c71a-216">Обратитесь к [группе поддержки BenefitHub](https://www.benefithub.com/Home/ContactUs), чтобы добавить пользователей на платформу BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="5c71a-217">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="5c71a-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c71a-218">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c71a-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c71a-219">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5c71a-221">**Чтобы назначить пользователя Britta Simon в BenefitHub, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="5c71a-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="5c71a-222">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5c71a-224">Из списка приложений выберите **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-224">In the applications list, select **BenefitHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="5c71a-226">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5c71a-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-228">Click **Add** button.</span></span> <span data-ttu-id="5c71a-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5c71a-231">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c71a-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c71a-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5c71a-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c71a-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5c71a-234">Testing single sign-on</span></span>

<span data-ttu-id="5c71a-235">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5c71a-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c71a-236">Щелкнув элемент "BenefitHub" на панели доступа, вы автоматически войдете в приложение BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5c71a-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="5c71a-237">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5c71a-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c71a-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5c71a-238">Additional resources</span></span>

* [<span data-ttu-id="5c71a-239">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c71a-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c71a-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c71a-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

