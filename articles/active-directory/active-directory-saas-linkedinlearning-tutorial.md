---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Learning | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и LinkedIn Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="794c7-103">Руководство по интеграции Azure Active Directory с LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="794c7-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="794c7-104">В этом руководстве описано, как интегрировать приложение LinkedIn Learning с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="794c7-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="794c7-105">Интеграция Azure AD с LinkedIn Learning обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="794c7-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="794c7-106">С помощью Azure AD вы можете контролировать доступ к LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="794c7-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="794c7-107">Вы можете включить автоматический вход пользователей в LinkedIn Learning (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="794c7-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="794c7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="794c7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="794c7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="794c7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="794c7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="794c7-110">Prerequisites</span></span>

<span data-ttu-id="794c7-111">Чтобы настроить интеграцию Azure AD с LinkedIn Learning, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="794c7-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="794c7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="794c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="794c7-113">подписка LinkedIn Learning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="794c7-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="794c7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="794c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="794c7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="794c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="794c7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="794c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="794c7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="794c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="794c7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="794c7-118">Scenario description</span></span>
<span data-ttu-id="794c7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="794c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="794c7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="794c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="794c7-121">Добавление LinkedIn Learning из коллекции</span><span class="sxs-lookup"><span data-stu-id="794c7-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="794c7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="794c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="794c7-123">Добавление LinkedIn Learning из коллекции</span><span class="sxs-lookup"><span data-stu-id="794c7-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="794c7-124">Чтобы настроить интеграцию LinkedIn Learning с Azure AD, необходимо добавить LinkedIn Learning из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="794c7-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="794c7-125">**Чтобы добавить LinkedIn Learning из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="794c7-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="794c7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="794c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="794c7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="794c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="794c7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="794c7-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="794c7-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="794c7-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="794c7-133">В поле поиска введите **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="794c7-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="794c7-134">На панели результатов щелкните **LinkedIn Learning**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="794c7-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="794c7-136">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="794c7-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="794c7-137">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Learning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="794c7-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="794c7-138">Для работы единого входа в Azure AD необходимо знать, какой пользователь в LinkedIn Learning соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="794c7-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="794c7-139">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="794c7-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="794c7-140">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="794c7-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="794c7-141">Чтобы настроить и проверить единый вход Azure AD в LinkedIn Learning, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="794c7-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="794c7-142">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="794c7-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="794c7-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="794c7-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="794c7-144">**[Создание тестового пользователя LinkedIn Learning](#creating-a-linkedin-learning-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="794c7-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="794c7-145">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="794c7-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="794c7-146">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="794c7-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="794c7-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="794c7-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="794c7-148">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="794c7-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="794c7-149">**Чтобы настроить единый вход Azure AD в LinkedIn Learning, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="794c7-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="794c7-150">На портале Azure на странице интеграции с приложением **LinkedIn Learning** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="794c7-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="794c7-152">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="794c7-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="794c7-154">В другом окне веб-браузера войдите в свой клиент LinkedIn Learning с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="794c7-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="794c7-155">В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="794c7-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="794c7-156">Также выберите **Learning - Default** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="794c7-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="794c7-158">Щелкните **OR Click Here to load and copy individual fields from the form** (Или щелкните здесь, чтобы загрузить и скопировать отдельные поля из формы) и скопируйте значения **Entity Id** (Идентификатор сущности) и **Assertion Consumer Service (ACS) Url** (URL-адрес службы обработчика утверждений (ACS)).</span><span class="sxs-lookup"><span data-stu-id="794c7-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="794c7-160">Если вы хотите настроить единый вход в режиме, **инициированном поставщиком удостоверений**, то на портале Azure в разделе **Домены и URL-адреса приложения LinkedIn Learning** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="794c7-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="794c7-162">а.</span><span class="sxs-lookup"><span data-stu-id="794c7-162">a.</span></span> <span data-ttu-id="794c7-163">В текстовом поле **Идентификатор** введите **идентификатор сущности**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="794c7-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="794c7-164">b.</span><span class="sxs-lookup"><span data-stu-id="794c7-164">b.</span></span> <span data-ttu-id="794c7-165">В текстовом поле **URL-адрес ответа** введите **URL-адрес службы обработчика утверждений (ACS)**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="794c7-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="794c7-166">Если вы хотите настроить единый вход в режиме, **инициированном поставщиком услуг**, то установите флажок "Показать дополнительные параметры URL-адресов" в разделе настроек и настройте URL-адрес входа в таком формате:</span><span class="sxs-lookup"><span data-stu-id="794c7-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="794c7-168">Приложение LinkedIn Learning ожидает утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="794c7-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="794c7-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="794c7-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="794c7-170">По умолчанию **идентификатор пользователя** имеет значение **user.userprincipalname**, но для LinkedIn Learning требуется сопоставить это значение с адресом электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="794c7-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="794c7-171">Для этого можно использовать атрибут **user.mail** из списка или соответствующее значение атрибута, основанное на конфигурации организации.</span><span class="sxs-lookup"><span data-stu-id="794c7-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="794c7-173">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и задайте эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="794c7-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="794c7-174">Пользователь должен добавить четыре утверждения — **email**, **department**, **firstname** и **lastname**, а их значения должны быть сопоставлены с **user.mail**, **user.department**, **user.givenname** и **user.surname**, соответственно</span><span class="sxs-lookup"><span data-stu-id="794c7-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="794c7-175">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="794c7-175">Attribute Name</span></span> | <span data-ttu-id="794c7-176">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="794c7-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="794c7-177">email</span><span class="sxs-lookup"><span data-stu-id="794c7-177">email</span></span>| <span data-ttu-id="794c7-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="794c7-178">user.mail</span></span> |    
    | <span data-ttu-id="794c7-179">department</span><span class="sxs-lookup"><span data-stu-id="794c7-179">department</span></span>| <span data-ttu-id="794c7-180">user.department</span><span class="sxs-lookup"><span data-stu-id="794c7-180">user.department</span></span> |
    | <span data-ttu-id="794c7-181">firstname</span><span class="sxs-lookup"><span data-stu-id="794c7-181">firstname</span></span>| <span data-ttu-id="794c7-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="794c7-182">user.givenname</span></span> |
    | <span data-ttu-id="794c7-183">lastname</span><span class="sxs-lookup"><span data-stu-id="794c7-183">lastname</span></span>| <span data-ttu-id="794c7-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="794c7-184">user.surname</span></span> |
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="794c7-186">а.</span><span class="sxs-lookup"><span data-stu-id="794c7-186">a.</span></span> <span data-ttu-id="794c7-187">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно атрибута.</span><span class="sxs-lookup"><span data-stu-id="794c7-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="794c7-190">b.</span><span class="sxs-lookup"><span data-stu-id="794c7-190">b.</span></span> <span data-ttu-id="794c7-191">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="794c7-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="794c7-192">c.</span><span class="sxs-lookup"><span data-stu-id="794c7-192">c.</span></span> <span data-ttu-id="794c7-193">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="794c7-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="794c7-194">d.</span><span class="sxs-lookup"><span data-stu-id="794c7-194">d.</span></span> <span data-ttu-id="794c7-195">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="794c7-195">Click **Ok**</span></span>

10. <span data-ttu-id="794c7-196">Выполните следующие действия с атрибутом **name**.</span><span class="sxs-lookup"><span data-stu-id="794c7-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="794c7-197">а.</span><span class="sxs-lookup"><span data-stu-id="794c7-197">a.</span></span> <span data-ttu-id="794c7-198">Щелкните атрибут, чтобы открыть окно **Изменить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="794c7-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="794c7-200">b.</span><span class="sxs-lookup"><span data-stu-id="794c7-200">b.</span></span> <span data-ttu-id="794c7-201">Удалите значение URL-адреса из **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="794c7-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="794c7-202">c.</span><span class="sxs-lookup"><span data-stu-id="794c7-202">c.</span></span> <span data-ttu-id="794c7-203">Нажмите кнопку **ОК**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="794c7-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="794c7-204">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="794c7-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="794c7-206">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="794c7-206">Click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="794c7-208">Перейдите в раздел **LinkedIn Admin Settings** (Параметры администратора LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="794c7-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="794c7-209">Отправьте XML-файл, скачанный с портала Azure. Для этого нажмите кнопку "Отправить XML-файл".</span><span class="sxs-lookup"><span data-stu-id="794c7-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="794c7-211">Нажмите кнопку **On** (Включить), чтобы включить единый вход.</span><span class="sxs-lookup"><span data-stu-id="794c7-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="794c7-212">Состояние единого входа изменяется с **Not Connected** (Не подключено) на **Connected** (Подключено.)</span><span class="sxs-lookup"><span data-stu-id="794c7-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="794c7-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="794c7-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="794c7-215">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="794c7-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="794c7-217">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="794c7-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="794c7-218">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="794c7-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="794c7-220">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="794c7-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="794c7-222">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="794c7-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="794c7-224">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="794c7-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="794c7-226">а.</span><span class="sxs-lookup"><span data-stu-id="794c7-226">a.</span></span> <span data-ttu-id="794c7-227">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="794c7-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="794c7-228">b.</span><span class="sxs-lookup"><span data-stu-id="794c7-228">b.</span></span> <span data-ttu-id="794c7-229">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="794c7-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="794c7-230">c.</span><span class="sxs-lookup"><span data-stu-id="794c7-230">c.</span></span> <span data-ttu-id="794c7-231">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="794c7-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="794c7-232">d.</span><span class="sxs-lookup"><span data-stu-id="794c7-232">d.</span></span> <span data-ttu-id="794c7-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="794c7-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="794c7-234">Создание тестового пользователя LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="794c7-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="794c7-235">Приложение Linked Learning поддерживает</span><span class="sxs-lookup"><span data-stu-id="794c7-235">Linked Learning Application supports.</span></span> <span data-ttu-id="794c7-236">своевременную подготовку (JIT-подготовку) пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="794c7-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="794c7-237">На странице параметров администратора на портале LinkedIn Learning включите параметр **Automatically assign licenses** (Автоматически назначать лицензии), чтобы активировать JIT-подготовку. При этом пользователю будет также назначена лицензия.</span><span class="sxs-lookup"><span data-stu-id="794c7-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="794c7-239">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="794c7-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="794c7-240">В этом разделе описано, как предоставить пользователю Britta Simon доступ к LinkedIn Learning, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="794c7-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="794c7-242">**Чтобы назначить пользователя Britta Simon в LinkedIn Learning, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="794c7-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="794c7-243">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="794c7-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="794c7-245">В списке приложений выберите **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="794c7-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="794c7-247">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="794c7-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="794c7-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="794c7-249">Click **Add** button.</span></span> <span data-ttu-id="794c7-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="794c7-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="794c7-252">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="794c7-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="794c7-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="794c7-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="794c7-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="794c7-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="794c7-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="794c7-255">Testing single sign-on</span></span>

<span data-ttu-id="794c7-256">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="794c7-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="794c7-257">Щелкнув элемент LinkedIn Learning на панели доступа, вы перейдете на страницу входа Azure и, успешного выполнив вход, войдете в приложение LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="794c7-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="794c7-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="794c7-258">Additional resources</span></span>

* [<span data-ttu-id="794c7-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="794c7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="794c7-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="794c7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png