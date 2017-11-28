---
title: "Руководство по интеграции Azure Active Directory с ADP eTime | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="ea941-103">Учебник. Интеграция Azure Active Directory с ADP eTime</span><span class="sxs-lookup"><span data-stu-id="ea941-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="ea941-104">В этом руководстве описано, как интегрировать ADP eTime с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea941-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea941-105">Интеграция ADP eTime с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ea941-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea941-106">С помощью Azure AD вы можете контролировать доступ к ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="ea941-107">Вы можете включить автоматический вход пользователей в ADP eTime (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea941-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea941-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ea941-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea941-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea941-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea941-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea941-110">Prerequisites</span></span>

<span data-ttu-id="ea941-111">Чтобы настроить интеграцию Azure AD с ADP eTime, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ea941-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="ea941-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ea941-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea941-113">подписка ADP eTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea941-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea941-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ea941-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea941-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ea941-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea941-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ea941-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea941-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea941-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea941-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ea941-118">Scenario description</span></span>
<span data-ttu-id="ea941-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ea941-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea941-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ea941-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea941-121">Добавление ADP eTime из коллекции</span><span class="sxs-lookup"><span data-stu-id="ea941-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="ea941-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea941-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="ea941-123">Добавление ADP eTime из коллекции</span><span class="sxs-lookup"><span data-stu-id="ea941-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="ea941-124">Чтобы настроить интеграцию ADP eTime с Azure AD, необходимо добавить ADP eTime из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea941-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea941-125">**Чтобы добавить ADP eTime из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ea941-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea941-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea941-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea941-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea941-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea941-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea941-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ea941-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ea941-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ea941-133">В поле поиска введите **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="ea941-133">In the search box, type **ADP eTime**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="ea941-135">На панели результатов выберите **ADP eTime** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ea941-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea941-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea941-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea941-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ADP eTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea941-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea941-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ADP eTime соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea941-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="ea941-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="ea941-141">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="ea941-142">Чтобы настроить и проверить единый вход Azure AD в ADP eTime, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ea941-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea941-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ea941-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea941-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea941-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea941-145">**[Создание тестового пользователя ADP eTime](#creating-an-adp-etime-test-user)** нужно для того, чтобы в ADP eTime также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea941-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea941-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea941-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea941-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea941-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea941-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea941-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea941-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="ea941-150">**Чтобы настроить единый вход Azure AD в ADP eTime, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ea941-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="ea941-151">На портале Azure на странице интеграции с приложением **ADP eTime** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ea941-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ea941-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea941-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="ea941-155">В разделе **Домены и URL-адреса приложения ADP eTime** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="ea941-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="ea941-157">а.</span><span class="sxs-lookup"><span data-stu-id="ea941-157">a.</span></span> <span data-ttu-id="ea941-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="ea941-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="ea941-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea941-159">b.</span></span> <span data-ttu-id="ea941-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`.</span><span class="sxs-lookup"><span data-stu-id="ea941-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="ea941-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ea941-161">These values are not the real.</span></span> <span data-ttu-id="ea941-162">Замените эти значения фактическим URL-адресом ответа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ea941-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="ea941-163">Чтобы получить эти значения, обратитесь к [группе поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea941-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="ea941-164">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea941-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="ea941-166">Приложение ADP eTime ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="ea941-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ea941-167">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="ea941-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ea941-168">Утверждение всегда будет носить имя **PersonImmutableID** и иметь значение, которое было сопоставлено с ExtensionAttribute2, содержащим EmployeeID пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea941-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="ea941-169">Здесь выполняется сопоставление пользователя из Azure AD с ADP eTime по значению EmployeeID, однако его можно сопоставить с другим значением, учитывая параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="ea941-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="ea941-170">Обратитесь к [группе поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx), чтобы указать правильный идентификатор пользователя и сопоставить это значение с утверждением **PersonImmutableID**.</span><span class="sxs-lookup"><span data-stu-id="ea941-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="ea941-172">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ea941-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ea941-173">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ea941-173">Attribute Name</span></span> | <span data-ttu-id="ea941-174">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ea941-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ea941-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="ea941-175">PersonImmutableID</span></span> | <span data-ttu-id="ea941-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="ea941-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="ea941-177">а.</span><span class="sxs-lookup"><span data-stu-id="ea941-177">a.</span></span> <span data-ttu-id="ea941-178">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="ea941-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ea941-181">b.</span><span class="sxs-lookup"><span data-stu-id="ea941-181">b.</span></span> <span data-ttu-id="ea941-182">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ea941-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ea941-183">c.</span><span class="sxs-lookup"><span data-stu-id="ea941-183">c.</span></span> <span data-ttu-id="ea941-184">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ea941-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ea941-185">г)</span><span class="sxs-lookup"><span data-stu-id="ea941-185">d.</span></span> <span data-ttu-id="ea941-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ea941-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea941-187">Чтобы настроить утверждение SAML, обратитесь к [группе поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) и запросите значение атрибута уникального идентификатора для своего клиента.</span><span class="sxs-lookup"><span data-stu-id="ea941-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="ea941-188">Это значение необходимо для настройки пользовательского утверждения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ea941-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="ea941-189">В разделе **Конфигурация ADP eTime** щелкните **Настроить ADP eTime**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ea941-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="ea941-191">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ea941-191">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ea941-193">Чтобы настроить единый вход на стороне **ADP eTime**, отправьте [группе поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="ea941-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="ea941-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ea941-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea941-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ea941-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea941-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ea941-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea941-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea941-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea941-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea941-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ea941-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ea941-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea941-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea941-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea941-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ea941-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea941-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ea941-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea941-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ea941-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea941-209">а.</span><span class="sxs-lookup"><span data-stu-id="ea941-209">a.</span></span> <span data-ttu-id="ea941-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea941-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea941-211">b.</span><span class="sxs-lookup"><span data-stu-id="ea941-211">b.</span></span> <span data-ttu-id="ea941-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea941-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea941-213">c.</span><span class="sxs-lookup"><span data-stu-id="ea941-213">c.</span></span> <span data-ttu-id="ea941-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ea941-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea941-215">d.</span><span class="sxs-lookup"><span data-stu-id="ea941-215">d.</span></span> <span data-ttu-id="ea941-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ea941-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="ea941-217">Создание тестового пользователя ADP eTime</span><span class="sxs-lookup"><span data-stu-id="ea941-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="ea941-218">Цель этого раздела — создать пользователя с именем Britta Simon в приложении ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="ea941-219">Обратитесь к [группе поддержки ADP eTime](https://www.adp.com/contact-us/overview.aspx), чтобы добавить пользователей в учетную запись ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea941-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea941-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea941-221">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ea941-223">**Чтобы назначить пользователя Britta Simon в ADP eTime, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ea941-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="ea941-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea941-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ea941-226">Из списка приложений выберите **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="ea941-226">In the applications list, select **ADP eTime**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="ea941-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ea941-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ea941-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ea941-230">Click **Add** button.</span></span> <span data-ttu-id="ea941-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ea941-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ea941-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ea941-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea941-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ea941-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea941-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ea941-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea941-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ea941-236">Testing single sign-on</span></span>

<span data-ttu-id="ea941-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ea941-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ea941-238">Щелкнув элемент ADP eTime на панели доступа, вы автоматически войдете в приложение ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="ea941-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="ea941-239">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea941-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ea941-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ea941-240">Additional resources</span></span>

* [<span data-ttu-id="ea941-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea941-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea941-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea941-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

