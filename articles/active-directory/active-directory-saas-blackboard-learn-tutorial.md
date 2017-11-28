---
title: "Руководство по интеграции Azure Active Directory с Blackboard Learn | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Blackboard Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="2703d-103">Учебник. Интеграция Azure Active Directory с Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="2703d-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="2703d-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2703d-105">Интеграция Blackboard Learn с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="2703d-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2703d-106">С помощью Azure AD вы можете контролировать доступ к Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="2703d-107">Вы можете включить автоматический вход пользователей в Blackboard Learn (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2703d-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2703d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2703d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2703d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2703d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2703d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2703d-110">Prerequisites</span></span>

<span data-ttu-id="2703d-111">Чтобы настроить интеграцию Azure AD с Blackboard Learn, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="2703d-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="2703d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2703d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2703d-113">подписка Blackboard Learn — Shibboleth с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2703d-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2703d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2703d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2703d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="2703d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2703d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2703d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2703d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2703d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2703d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2703d-118">Scenario description</span></span>
<span data-ttu-id="2703d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2703d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2703d-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="2703d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2703d-121">Добавление Blackboard Learn из коллекции</span><span class="sxs-lookup"><span data-stu-id="2703d-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="2703d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2703d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="2703d-123">Добавление Blackboard Learn из коллекции</span><span class="sxs-lookup"><span data-stu-id="2703d-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="2703d-124">Чтобы настроить интеграцию Blackboard Learn с Azure AD, необходимо добавить Blackboard Learn из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2703d-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2703d-125">**Чтобы добавить Blackboard Learn из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="2703d-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2703d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2703d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2703d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2703d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2703d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2703d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="2703d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="2703d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="2703d-133">В поле поиска введите **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="2703d-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="2703d-135">В области результатов выберите **Blackboard Learn** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="2703d-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2703d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2703d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2703d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Blackboard Learn с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2703d-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2703d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Blackboard Learn соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2703d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="2703d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="2703d-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="2703d-142">Чтобы настроить и проверить единый вход Azure AD в Blackboard Learn, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="2703d-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2703d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="2703d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2703d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2703d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2703d-145">**[Создание тестового пользователя Blackboard Learn](#creating-a-blackboard-learn-test-user)** нужно для того, чтобы в Blackboard Learn также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2703d-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2703d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2703d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2703d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2703d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2703d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2703d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2703d-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="2703d-150">**Чтобы настроить единый вход Azure AD в Blackboard Learn, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="2703d-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="2703d-151">На портале Azure на странице интеграции с приложением **Blackboard Learn** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="2703d-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="2703d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="2703d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="2703d-155">В разделе **Домены и URL-адреса приложения Blackboard Learn** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2703d-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="2703d-157">а.</span><span class="sxs-lookup"><span data-stu-id="2703d-157">a.</span></span> <span data-ttu-id="2703d-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="2703d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="2703d-159">b.</span><span class="sxs-lookup"><span data-stu-id="2703d-159">b.</span></span> <span data-ttu-id="2703d-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="2703d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2703d-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="2703d-161">These values are not real.</span></span> <span data-ttu-id="2703d-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="2703d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2703d-163">Чтобы получить эти значения, обратитесь к [группе поддержки Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="2703d-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="2703d-164">Приложение Blackboard Learn ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="2703d-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2703d-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="2703d-165">Configure the following claims for this application.</span></span> <span data-ttu-id="2703d-166">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="2703d-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="2703d-167">На следующем снимке экрана показан пример.</span><span class="sxs-lookup"><span data-stu-id="2703d-167">The following screenshot shows an example about it.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="2703d-169">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2703d-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="2703d-170">Мы сопоставили Userprincipalname как уникальный атрибут пользователя, но вы можете сопоставить его с соответствующим значением, которое однозначно идентифицирует пользователя в организации и сопоставляется с полем имени пользователя Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="2703d-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="2703d-171">Attribute Name</span></span> | <span data-ttu-id="2703d-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="2703d-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="2703d-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="2703d-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="2703d-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="2703d-174">user.userprincipalname</span></span> |

    <span data-ttu-id="2703d-175">а.</span><span class="sxs-lookup"><span data-stu-id="2703d-175">a.</span></span> <span data-ttu-id="2703d-176">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="2703d-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2703d-179">b.</span><span class="sxs-lookup"><span data-stu-id="2703d-179">b.</span></span> <span data-ttu-id="2703d-180">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="2703d-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2703d-181">c.</span><span class="sxs-lookup"><span data-stu-id="2703d-181">c.</span></span> <span data-ttu-id="2703d-182">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="2703d-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="2703d-183">г)</span><span class="sxs-lookup"><span data-stu-id="2703d-183">d.</span></span> <span data-ttu-id="2703d-184">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2703d-184">Click **Ok**.</span></span>

4. <span data-ttu-id="2703d-185">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2703d-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="2703d-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2703d-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2703d-189">В разделе **Конфигурация Blackboard Learn** щелкните **Настроить Blackboard Learn**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2703d-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2703d-190">Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="2703d-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="2703d-192">Для настройки единого входа на стороне приложения **Blackboard Learn** необходимо отправить скачанный **XML-файл метаданных** и **идентификатор сущности SAML** [группе поддержки Blackboard Learn](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="2703d-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="2703d-193">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="2703d-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2703d-194">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2703d-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2703d-195">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2703d-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2703d-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2703d-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="2703d-197">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2703d-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="2703d-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2703d-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2703d-200">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2703d-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2703d-202">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="2703d-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2703d-204">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2703d-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2703d-206">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2703d-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2703d-208">а.</span><span class="sxs-lookup"><span data-stu-id="2703d-208">a.</span></span> <span data-ttu-id="2703d-209">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2703d-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2703d-210">b.</span><span class="sxs-lookup"><span data-stu-id="2703d-210">b.</span></span> <span data-ttu-id="2703d-211">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2703d-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="2703d-212">c.</span><span class="sxs-lookup"><span data-stu-id="2703d-212">c.</span></span> <span data-ttu-id="2703d-213">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="2703d-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2703d-214">d.</span><span class="sxs-lookup"><span data-stu-id="2703d-214">d.</span></span> <span data-ttu-id="2703d-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2703d-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="2703d-216">Создание тестового пользователя Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="2703d-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="2703d-217">В этом разделе описано, как создать пользователя Britta Simon в приложении Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="2703d-218">Приложение Blackboard Learn поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="2703d-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="2703d-219">Убедитесь, что утверждения настроены, как описано в разделе **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="2703d-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2703d-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2703d-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2703d-221">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="2703d-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2703d-223">**Чтобы назначить пользователя Britta Simon в Blackboard Learn, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="2703d-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="2703d-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2703d-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2703d-226">В списке приложений выберите **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="2703d-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="2703d-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2703d-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="2703d-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2703d-230">Click **Add** button.</span></span> <span data-ttu-id="2703d-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2703d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="2703d-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2703d-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2703d-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2703d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2703d-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2703d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2703d-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2703d-236">Testing single sign-on</span></span>

<span data-ttu-id="2703d-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2703d-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2703d-238">Щелкнув элемент "Blackboard Learn — Shibboleth" на панели доступа, вы автоматически войдете в приложение Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="2703d-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="2703d-239">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2703d-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2703d-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2703d-240">Additional resources</span></span>

* [<span data-ttu-id="2703d-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2703d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2703d-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2703d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

