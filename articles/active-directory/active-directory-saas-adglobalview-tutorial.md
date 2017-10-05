---
title: "Руководство по интеграции Azure Active Directory с ADP Globalview | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="30115-103">Руководство по интеграции Azure Active Directory с ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="30115-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="30115-104">В этом руководстве описано, как интегрировать ADP Globalview с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30115-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30115-105">Интеграция Azure AD с ADP Globalview обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="30115-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="30115-106">С помощью Azure AD вы можете контролировать доступ к ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="30115-107">Вы можете включить автоматический вход пользователей в ADP Globalview (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30115-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30115-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30115-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="30115-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30115-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30115-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="30115-110">Prerequisites</span></span>

<span data-ttu-id="30115-111">Чтобы настроить интеграцию Azure AD с ADP Globalview, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="30115-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="30115-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="30115-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30115-113">подписка ADP Globalview с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="30115-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30115-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="30115-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30115-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="30115-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30115-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="30115-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30115-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30115-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30115-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="30115-118">Scenario description</span></span>
<span data-ttu-id="30115-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="30115-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30115-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="30115-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30115-121">Добавление ADP Globalview из коллекции</span><span class="sxs-lookup"><span data-stu-id="30115-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="30115-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="30115-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="30115-123">Добавление ADP Globalview из коллекции</span><span class="sxs-lookup"><span data-stu-id="30115-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="30115-124">Чтобы настроить интеграцию ADP Globalview с Azure AD, необходимо добавить ADP Globalview из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="30115-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="30115-125">**Чтобы добавить ADP Globalview из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="30115-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="30115-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30115-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30115-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="30115-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="30115-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="30115-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="30115-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="30115-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="30115-133">В поле поиска введите **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="30115-133">In the search box, type **ADP Globalview**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="30115-135">На панели результатов выберите **ADP Globalview** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="30115-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30115-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="30115-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30115-138">В этом разделе описана настройка и проверка единого входа Azure AD в ADP Globalview с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30115-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="30115-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ADP Globalview соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30115-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="30115-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="30115-141">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="30115-142">Чтобы настроить и проверить единый вход Azure AD в ADP Globalview, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="30115-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="30115-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="30115-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="30115-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30115-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30115-145">**[Создание тестового пользователя ADP Globalview](#creating-an-adp-globalview-test-user)** нужно для того, чтобы в ADP Globalview также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30115-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="30115-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30115-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30115-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="30115-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30115-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="30115-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30115-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="30115-150">**Чтобы настроить единый вход Azure AD в ADP Globalview, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="30115-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="30115-151">На портале Azure на странице интеграции с приложением **ADP Globalview** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="30115-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="30115-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="30115-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="30115-155">В разделе **Домены и URL-адреса приложения ADP Globalview** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="30115-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="30115-157">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.globalview.adp.com/federate` или `https://<subdomain>.globalview.adp.com/federate2`.</span><span class="sxs-lookup"><span data-stu-id="30115-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30115-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="30115-158">The value is not real.</span></span> <span data-ttu-id="30115-159">Вместо него нужно указать фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="30115-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="30115-160">Обратитесь в [службу поддержки ADP Globalview](https://www.adp.com/contact-us/overview.aspx) для получения этого значения.</span><span class="sxs-lookup"><span data-stu-id="30115-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="30115-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="30115-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="30115-163">Приложение ADP Globalview ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="30115-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="30115-164">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="30115-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="30115-165">Утверждение всегда будет носить имя **PersonImmutableID** и иметь значение, которое было сопоставлено с ExtensionAttribute2, содержащим EmployeeID пользователя.</span><span class="sxs-lookup"><span data-stu-id="30115-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="30115-166">Здесь выполняется сопоставление пользователя из Azure AD с ADP Globalview по значению EmployeeID, однако его можно сопоставить с другим значением, учитывая параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="30115-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="30115-167">Вместе со службой поддержки ADP GlobalView выполните действия по использованию правильного идентификатора пользователя и его сопоставлению с утверждением **PersonImmutableID**.</span><span class="sxs-lookup"><span data-stu-id="30115-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="30115-168">Также можно сопоставить утверждения электронной почты и идентификатора пользователя, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="30115-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="30115-170">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="30115-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="30115-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="30115-171">Attribute Name</span></span> | <span data-ttu-id="30115-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="30115-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="30115-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="30115-173">personalimmutableid</span></span> | <span data-ttu-id="30115-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="30115-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="30115-175">email</span><span class="sxs-lookup"><span data-stu-id="30115-175">email</span></span>               | <span data-ttu-id="30115-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="30115-176">user.mail</span></span> |
    | <span data-ttu-id="30115-177">userid</span><span class="sxs-lookup"><span data-stu-id="30115-177">userid</span></span>              | <span data-ttu-id="30115-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="30115-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="30115-179">а.</span><span class="sxs-lookup"><span data-stu-id="30115-179">a.</span></span> <span data-ttu-id="30115-180">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="30115-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="30115-183">b.</span><span class="sxs-lookup"><span data-stu-id="30115-183">b.</span></span> <span data-ttu-id="30115-184">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="30115-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="30115-185">c.</span><span class="sxs-lookup"><span data-stu-id="30115-185">c.</span></span> <span data-ttu-id="30115-186">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="30115-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="30115-187">г)</span><span class="sxs-lookup"><span data-stu-id="30115-187">d.</span></span> <span data-ttu-id="30115-188">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="30115-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30115-189">Чтобы настроить утверждение SAML, обратитесь в [службу поддержки ADP Globalview](https://www.adp.com/contact-us/overview.aspx) и запросите значение атрибута уникального идентификатора для своего клиента.</span><span class="sxs-lookup"><span data-stu-id="30115-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="30115-190">Это значение необходимо для настройки пользовательского утверждения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="30115-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="30115-191">В разделе **Конфигурация ADP Globalview** щелкните **Настроить ADP Globalview**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="30115-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="30115-192">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="30115-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="30115-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="30115-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="30115-196">Чтобы настроить единый вход на стороне **ADP Globalview**, нужно отправить скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="30115-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="30115-197">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="30115-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="30115-198">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="30115-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="30115-199">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="30115-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30115-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="30115-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="30115-201">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30115-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="30115-203">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="30115-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="30115-204">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30115-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="30115-206">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="30115-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30115-208">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="30115-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30115-210">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="30115-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30115-212">а.</span><span class="sxs-lookup"><span data-stu-id="30115-212">a.</span></span> <span data-ttu-id="30115-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30115-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30115-214">b.</span><span class="sxs-lookup"><span data-stu-id="30115-214">b.</span></span> <span data-ttu-id="30115-215">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30115-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30115-216">c.</span><span class="sxs-lookup"><span data-stu-id="30115-216">c.</span></span> <span data-ttu-id="30115-217">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="30115-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="30115-218">d.</span><span class="sxs-lookup"><span data-stu-id="30115-218">d.</span></span> <span data-ttu-id="30115-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="30115-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="30115-220">Создание тестового пользователя ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="30115-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="30115-221">Цель этого раздела — создать пользователя с именем Britta Simon в приложении ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="30115-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="30115-222">Обратитесь в [службу поддержки ADP Globalview](https://www.adp.com/contact-us/overview.aspx), чтобы добавить пользователей в учетную запись ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="30115-223">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="30115-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="30115-224">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="30115-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="30115-226">**Чтобы назначить пользователя Britta Simon в ADP Globalview, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="30115-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="30115-227">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="30115-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="30115-229">Из списка приложений выберите **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="30115-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="30115-231">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="30115-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="30115-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="30115-233">Click **Add** button.</span></span> <span data-ttu-id="30115-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="30115-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="30115-236">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="30115-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="30115-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="30115-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30115-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="30115-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30115-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="30115-239">Testing single sign-on</span></span>

<span data-ttu-id="30115-240">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="30115-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="30115-241">Щелкнув элемент ADP GlobalView на панели доступа, вы автоматически войдете в приложение ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="30115-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30115-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="30115-242">Additional resources</span></span>

* [<span data-ttu-id="30115-243">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30115-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30115-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="30115-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

