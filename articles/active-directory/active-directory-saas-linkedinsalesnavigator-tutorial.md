---
title: "Учебник. Интеграция Azure Active Directory с LinkedInSalesNavigator | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: ef26a16e79d9c9b0654634960b57dc59827b2c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="16563-103">Руководство по интеграции Azure Active Directory с LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="16563-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="16563-104">В этом руководстве описано, как интегрировать приложение LinkedIn Sales Navigator с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16563-104">In this tutorial, you learn how to integrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16563-105">Интеграция Azure AD с LinkedIn Sales Navigator обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="16563-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16563-106">С помощью Azure AD вы можете контролировать доступ к LinLinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="16563-106">You can control in Azure AD who has access to LinkedIn Sales Navigator</span></span>
- <span data-ttu-id="16563-107">Вы можете включить автоматический вход пользователей в LinkedIn Sales Navigator (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16563-107">You can enable your users to automatically get signed-on to LinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16563-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="16563-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16563-109">Подробнее об интеграции приложений SaaS с Azure AD можно узнать в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16563-109">If you want to know more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16563-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="16563-110">Prerequisites</span></span>

<span data-ttu-id="16563-111">Чтобы настроить интеграцию Azure AD с LinkedIn Sales Navigator, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="16563-111">To configure Azure AD integration with LinkedIn Sales Navigator, you need the following items:</span></span>

- <span data-ttu-id="16563-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="16563-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16563-113">подписка LinkedIn Sales Navigator с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="16563-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16563-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="16563-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16563-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="16563-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16563-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="16563-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16563-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16563-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16563-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="16563-118">Scenario description</span></span>
<span data-ttu-id="16563-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="16563-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16563-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="16563-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16563-121">Добавление LinkedIn Sales Navigator из коллекции</span><span class="sxs-lookup"><span data-stu-id="16563-121">Adding LinkedIn Sales Navigator from the gallery</span></span>
2. <span data-ttu-id="16563-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="16563-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-the-gallery"></a><span data-ttu-id="16563-123">Добавление LinkedIn Sales Navigator из коллекции</span><span class="sxs-lookup"><span data-stu-id="16563-123">Adding LinkedIn Sales Navigator from the gallery</span></span>
<span data-ttu-id="16563-124">Чтобы настроить интеграцию LinkedIn Sales Navigator с Azure AD, нужно добавить LinkedIn Sales Navigator из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="16563-124">To configure the integration of LinkedIn Sales Navigator into Azure AD, you need to add LinkedIn Sales Navigator from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16563-125">**Чтобы добавить LinkedIn Sales Navigator из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="16563-125">**To add LinkedIn Sales Navigator from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16563-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16563-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16563-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="16563-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16563-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="16563-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="16563-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="16563-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="16563-133">В поле поиска введите **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="16563-133">In the search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="16563-135">На панели результатов выберите **LinkedIn Sales Navigator** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="16563-135">In the results panel, select **LinkedIn Sales Navigator**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16563-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="16563-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16563-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Sales Navigator с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16563-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="16563-139">Для работы единого входа в Azure AD нужно знать, какой пользователь в LinkedIn Sales Navigator соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16563-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Sales Navigator is to a user in Azure AD.</span></span> <span data-ttu-id="16563-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="16563-140">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Sales Navigator needs to be established.</span></span>

<span data-ttu-id="16563-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="16563-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="16563-142">Чтобы настроить и проверить единый вход Azure AD в LinkedIn Sales Navigator, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="16563-142">To configure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16563-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="16563-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16563-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16563-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16563-145">**[Создание тестового пользователя LinkedIn Sales Navigator](#creating-a-linkedin-sales-navigator-test-user)** требуется для создания пользователя Britta Simon в LinkedIn Sales Navigator, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16563-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - to have a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="16563-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16563-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16563-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="16563-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16563-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="16563-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16563-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="16563-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="16563-150">**Чтобы настроить единый вход Azure AD в LinkedIn Sales Navigator, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="16563-150">**To configure Azure AD single sign-on with LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="16563-151">На портале Azure на странице интеграции с приложением **LinkedIn Sales Navigator** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="16563-151">In the Azure portal, on the **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="16563-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="16563-153">On the **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="16563-155">В другом окне веб-браузера войдите на свой веб-сайт **LinkedIn Sales Navigator** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="16563-155">In a different web browser window, sign-on to your **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="16563-156">В разделе **Параметры** **Центра управления учетной записью** щелкните **Глобальные параметры**.</span><span class="sxs-lookup"><span data-stu-id="16563-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="16563-157">Также выберите **Sales Navigator** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="16563-157">Also, select **Sales Navigator** from the dropdown list.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="16563-159">Щелкните **OR Click Here to load and copy individual fields from the form** (Или щелкните здесь, чтобы загрузить и скопировать отдельные поля из формы) и скопируйте значения **Entity Id** (Идентификатор сущности) и **Assertion Consumer Service (ACS) Url** (URL-адрес службы обработчика утверждений (ACS)).</span><span class="sxs-lookup"><span data-stu-id="16563-159">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="16563-161">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения LinkedIn Sales Navigator** портала Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="16563-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="16563-163">а.</span><span class="sxs-lookup"><span data-stu-id="16563-163">a.</span></span> <span data-ttu-id="16563-164">В текстовом поле **Идентификатор** введите **идентификатор сущности**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="16563-164">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="16563-165">b.</span><span class="sxs-lookup"><span data-stu-id="16563-165">b.</span></span> <span data-ttu-id="16563-166">В текстовом поле **URL-адрес ответа** введите **URL-адрес службы обработчика утверждений (ACS)**, скопированный с портала LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="16563-166">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="16563-167">Установите флажок **Показать дополнительные параметры URL-адресов**, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="16563-167">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="16563-169">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`.</span><span class="sxs-lookup"><span data-stu-id="16563-169">In the **Sign-on URL** textbox, type the value using the following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="16563-170">Приложение **LinkedIn Sales Navigator** ожидает утверждения SAML в определенном формате, а для этого вам нужно добавить настраиваемые сопоставления атрибутов в конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="16563-170">Your **LinkedIn Sales Navigator** application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="16563-171">На следующем снимке экрана показан пример.</span><span class="sxs-lookup"><span data-stu-id="16563-171">The following screenshot shows an example.</span></span> <span data-ttu-id="16563-172">По умолчанию **идентификатор пользователя** имеет значение **user.userprincipalname**, но для LinkedIn Sales Navigator требуется сопоставить это значение с адресом электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="16563-172">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it to be mapped with the user's email address.</span></span> <span data-ttu-id="16563-173">Можно использовать атрибут **user.mail** из списка или соответствующее значение атрибута, основанное на конфигурации организации.</span><span class="sxs-lookup"><span data-stu-id="16563-173">You can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="16563-175">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей** и задайте эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="16563-175">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="16563-176">Пользователь должен добавить четыре утверждения — **email**, **department**, **firstname** и **lastname**, а их значения должны быть сопоставлены с **user.mail**, **user.department**, **user.givenname** и **user.surname**, соответственно</span><span class="sxs-lookup"><span data-stu-id="16563-176">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="16563-177">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="16563-177">Attribute Name</span></span> | <span data-ttu-id="16563-178">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="16563-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="16563-179">email</span><span class="sxs-lookup"><span data-stu-id="16563-179">email</span></span>| <span data-ttu-id="16563-180">user.mail</span><span class="sxs-lookup"><span data-stu-id="16563-180">user.mail</span></span> |
    | <span data-ttu-id="16563-181">department</span><span class="sxs-lookup"><span data-stu-id="16563-181">department</span></span>| <span data-ttu-id="16563-182">user.department</span><span class="sxs-lookup"><span data-stu-id="16563-182">user.department</span></span> |
    | <span data-ttu-id="16563-183">firstname</span><span class="sxs-lookup"><span data-stu-id="16563-183">firstname</span></span>| <span data-ttu-id="16563-184">user.givenname</span><span class="sxs-lookup"><span data-stu-id="16563-184">user.givenname</span></span> |
    | <span data-ttu-id="16563-185">lastname</span><span class="sxs-lookup"><span data-stu-id="16563-185">lastname</span></span>| <span data-ttu-id="16563-186">user.surname</span><span class="sxs-lookup"><span data-stu-id="16563-186">user.surname</span></span> |
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="16563-188">а.</span><span class="sxs-lookup"><span data-stu-id="16563-188">a.</span></span> <span data-ttu-id="16563-189">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно атрибута.</span><span class="sxs-lookup"><span data-stu-id="16563-189">Click on **Add Attribute** to open the attribute dialog.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="16563-192">b.</span><span class="sxs-lookup"><span data-stu-id="16563-192">b.</span></span> <span data-ttu-id="16563-193">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="16563-193">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="16563-194">c.</span><span class="sxs-lookup"><span data-stu-id="16563-194">c.</span></span> <span data-ttu-id="16563-195">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="16563-195">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="16563-196">d.</span><span class="sxs-lookup"><span data-stu-id="16563-196">d.</span></span> <span data-ttu-id="16563-197">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="16563-197">Click **Ok**</span></span>

10. <span data-ttu-id="16563-198">Выполните следующие действия с атрибутом **name**.</span><span class="sxs-lookup"><span data-stu-id="16563-198">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="16563-199">а.</span><span class="sxs-lookup"><span data-stu-id="16563-199">a.</span></span> <span data-ttu-id="16563-200">Щелкните атрибут, чтобы открыть окно **Изменить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="16563-200">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="16563-202">b.</span><span class="sxs-lookup"><span data-stu-id="16563-202">b.</span></span> <span data-ttu-id="16563-203">Удалите значение URL-адреса из **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="16563-203">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="16563-204">c.</span><span class="sxs-lookup"><span data-stu-id="16563-204">c.</span></span> <span data-ttu-id="16563-205">Нажмите кнопку **ОК**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="16563-205">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="16563-206">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="16563-206">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="16563-208">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="16563-208">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="16563-210">Перейдите в раздел **LinkedIn Admin Settings** (Параметры администратора LinkedIn).</span><span class="sxs-lookup"><span data-stu-id="16563-210">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="16563-211">Щелкните **Upload XML file** (Отправить XML-файл), чтобы отправить XML-файл метаданных, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="16563-211">Click **Upload XML file** to upload the Metadata XML file that you have downloaded from the Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="16563-213">Нажмите кнопку **On** (Включить), чтобы включить единый вход.</span><span class="sxs-lookup"><span data-stu-id="16563-213">Click **On** to enable SSO.</span></span> <span data-ttu-id="16563-214">Состояние единого входа изменяется с **Not Connected** (Не подключено) на **Connected** (Подключено.)</span><span class="sxs-lookup"><span data-stu-id="16563-214">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="16563-216">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="16563-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16563-217">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="16563-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16563-218">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="16563-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16563-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="16563-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="16563-220">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16563-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="16563-222">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="16563-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16563-223">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16563-223">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16563-225">Перейдите в раздел **Пользователи и группы** и выберите **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="16563-225">Go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16563-227">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="16563-227">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16563-229">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16563-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16563-231">а.</span><span class="sxs-lookup"><span data-stu-id="16563-231">a.</span></span> <span data-ttu-id="16563-232">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16563-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16563-233">b.</span><span class="sxs-lookup"><span data-stu-id="16563-233">b.</span></span> <span data-ttu-id="16563-234">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="16563-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16563-235">c.</span><span class="sxs-lookup"><span data-stu-id="16563-235">c.</span></span> <span data-ttu-id="16563-236">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="16563-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16563-237">d.</span><span class="sxs-lookup"><span data-stu-id="16563-237">d.</span></span> <span data-ttu-id="16563-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="16563-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="16563-239">Создание тестового пользователя LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="16563-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="16563-240">Приложение LinkedIn Sales Navigator поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи создаются в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="16563-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="16563-241">Включите параметр **Automatically assign licenses** (Автоматически назначать лицензии), чтобы назначить лицензию пользователю.</span><span class="sxs-lookup"><span data-stu-id="16563-241">Activate **Automatically assign licenses** to assign a license to the user.</span></span>
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16563-243">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="16563-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16563-244">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="16563-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Sales Navigator.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="16563-246">**Чтобы назначить пользователя Britta Simon в LinkedIn Sales Navigator, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="16563-246">**To assign Britta Simon to LinkedIn Sales Navigator, perform the following steps:**</span></span>

1. <span data-ttu-id="16563-247">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="16563-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="16563-249">В списке приложений выберите **LinkedIn Sales Navigator**.</span><span class="sxs-lookup"><span data-stu-id="16563-249">In the applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="16563-251">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="16563-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="16563-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="16563-253">Click **Add** button.</span></span> <span data-ttu-id="16563-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="16563-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="16563-256">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="16563-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16563-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="16563-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16563-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="16563-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16563-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="16563-259">Testing single sign-on</span></span>

<span data-ttu-id="16563-260">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="16563-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="16563-261">При щелчке элемента LinkedIn Sales Navigator на панели доступа должна открыться страница организации, где нужно указать сведения о личной учетной записи LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="16563-261">When you click the LinkedIn Sales Navigator tile in the Access Panel, you should be redirected to Organizational page where you have to provide your personal LinkedIn account details.</span></span> <span data-ttu-id="16563-262">В результате ваша личная учетная запись связывается с вашей рабочей учетной записью LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="16563-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="16563-263">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="16563-263">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16563-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="16563-264">Additional resources</span></span>

* [<span data-ttu-id="16563-265">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16563-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16563-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="16563-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

