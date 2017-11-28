---
title: "Руководство по интеграции Azure Active Directory с приложением Slack | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="8d22b-103">Учебник. Интеграция Azure Active Directory с Slack</span><span class="sxs-lookup"><span data-stu-id="8d22b-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="8d22b-104">В этом руководстве описано, как интегрировать Slack с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d22b-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d22b-105">Интеграция Azure AD с приложением Slack обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="8d22b-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d22b-106">С помощью Azure AD вы можете контролировать доступ к Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="8d22b-107">Вы можете включить автоматический вход пользователей в Slack (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d22b-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d22b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d22b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d22b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d22b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d22b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d22b-110">Prerequisites</span></span>

<span data-ttu-id="8d22b-111">Чтобы настроить интеграцию Azure AD с Slack, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8d22b-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="8d22b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8d22b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d22b-113">подписка Slack с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d22b-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d22b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8d22b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d22b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8d22b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d22b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8d22b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d22b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d22b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d22b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8d22b-118">Scenario description</span></span>
<span data-ttu-id="8d22b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8d22b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d22b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8d22b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d22b-121">Добавление Slack из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8d22b-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="8d22b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d22b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="8d22b-123">Добавление Slack из коллекции</span><span class="sxs-lookup"><span data-stu-id="8d22b-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="8d22b-124">Чтобы настроить интеграцию Slack с Azure AD, необходимо добавить Slack из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d22b-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d22b-125">**Чтобы добавить Slack из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8d22b-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d22b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d22b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d22b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8d22b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8d22b-133">В поле поиска введите **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-133">In the search box, type **Slack**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="8d22b-135">На панели результатов выберите **Slack** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="8d22b-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d22b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d22b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d22b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Slack с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d22b-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d22b-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Slack соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d22b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="8d22b-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="8d22b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d22b-142">Чтобы настроить и проверить единый вход Azure AD в Slack, нужно выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="8d22b-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d22b-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8d22b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d22b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d22b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d22b-145">**[Создание тестового пользователя Slack](#creating-a-slack-test-user)** требуется для того, чтобы в Slack существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d22b-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d22b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d22b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d22b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d22b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d22b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d22b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d22b-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="8d22b-150">**Чтобы настроить единый вход Azure AD в Slack, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8d22b-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8d22b-151">На портале Azure на странице интеграции с приложением **Slack** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8d22b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d22b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="8d22b-155">В разделе **Домены и URL-адреса приложения Slack** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8d22b-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="8d22b-157">а.</span><span class="sxs-lookup"><span data-stu-id="8d22b-157">a.</span></span> <span data-ttu-id="8d22b-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="8d22b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="8d22b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d22b-159">b.</span></span> <span data-ttu-id="8d22b-160">В текстовом поле **Идентификатор** введите URL-адрес `https://slack.com`.</span><span class="sxs-lookup"><span data-stu-id="8d22b-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d22b-161">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="8d22b-161">The value is not real.</span></span> <span data-ttu-id="8d22b-162">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="8d22b-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="8d22b-163">Чтобы получить это значение, обратитесь к [группе поддержки Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="8d22b-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="8d22b-164">Приложение Slack ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="8d22b-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8d22b-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="8d22b-165">Configure the following claims for this application.</span></span> <span data-ttu-id="8d22b-166">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="8d22b-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8d22b-167">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="8d22b-167">The following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="8d22b-169">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** выберите значение **user.mail** для параметра **Идентификатор пользователя**, а в каждой строке в таблице ниже выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8d22b-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="8d22b-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="8d22b-170">Attribute Name</span></span> | <span data-ttu-id="8d22b-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="8d22b-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="8d22b-172">first_name</span><span class="sxs-lookup"><span data-stu-id="8d22b-172">first_name</span></span> | <span data-ttu-id="8d22b-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8d22b-173">user.givenname</span></span> |
    | <span data-ttu-id="8d22b-174">last_name</span><span class="sxs-lookup"><span data-stu-id="8d22b-174">last_name</span></span> | <span data-ttu-id="8d22b-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="8d22b-175">user.surname</span></span> |
    | <span data-ttu-id="8d22b-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="8d22b-176">User.Email</span></span> | <span data-ttu-id="8d22b-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="8d22b-177">user.mail</span></span> |  
    | <span data-ttu-id="8d22b-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="8d22b-178">User.Username</span></span> | <span data-ttu-id="8d22b-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8d22b-179">user.userprincipalname</span></span> |

    <span data-ttu-id="8d22b-180">а.</span><span class="sxs-lookup"><span data-stu-id="8d22b-180">a.</span></span> <span data-ttu-id="8d22b-181">Щелкните **Атрибут**, чтобы открыть диалоговое окно **Изменить атрибут**, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8d22b-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="8d22b-183">а.</span><span class="sxs-lookup"><span data-stu-id="8d22b-183">a.</span></span> <span data-ttu-id="8d22b-184">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8d22b-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8d22b-185">b.</span><span class="sxs-lookup"><span data-stu-id="8d22b-185">b.</span></span> <span data-ttu-id="8d22b-186">Из списка **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="8d22b-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8d22b-187">c.</span><span class="sxs-lookup"><span data-stu-id="8d22b-187">c.</span></span> <span data-ttu-id="8d22b-188">Щелкните **ОК**</span><span class="sxs-lookup"><span data-stu-id="8d22b-188">Click **OK**</span></span>

6. <span data-ttu-id="8d22b-189">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d22b-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="8d22b-191">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8d22b-191">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8d22b-193">В разделе **Конфигурация Slack** щелкните **Настроить Slack**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d22b-194">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="8d22b-196">В другом окне веб-браузера войдите на свой корпоративный сайт Slack в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8d22b-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="8d22b-197">Выберите **Microsoft Azure AD** > **Team Settings** (Параметры команды).</span><span class="sxs-lookup"><span data-stu-id="8d22b-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="8d22b-199">В разделе **Team Settings** (Параметры команды) выберите вкладку **Authentication** (Проверка подлинности) и нажмите кнопку **Change Settings** (Изменить параметры).</span><span class="sxs-lookup"><span data-stu-id="8d22b-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="8d22b-201">На странице **Параметры проверки подлинности SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8d22b-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="8d22b-203">а.</span><span class="sxs-lookup"><span data-stu-id="8d22b-203">a.</span></span>  <span data-ttu-id="8d22b-204">В текстовое поле **SAML 2.0 Endpoint (HTTP)** (Конечная точка SAML 2.0 (HTTP)) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8d22b-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8d22b-205">b.</span><span class="sxs-lookup"><span data-stu-id="8d22b-205">b.</span></span>  <span data-ttu-id="8d22b-206">В текстовое поле **Identity Provider Issuer** (Издатель поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8d22b-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8d22b-207">c.</span><span class="sxs-lookup"><span data-stu-id="8d22b-207">c.</span></span>  <span data-ttu-id="8d22b-208">Откройте скачанный файл сертификата в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Public Certificate** (Общий сертификат).</span><span class="sxs-lookup"><span data-stu-id="8d22b-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="8d22b-209">г)</span><span class="sxs-lookup"><span data-stu-id="8d22b-209">d.</span></span> <span data-ttu-id="8d22b-210">Настройте три показанных выше параметра для своей группы Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="8d22b-211">Дополнительные сведения о параметрах см. в статье **Guide to single sign-on with Slack** (Руководство по настройке единого входа в Slack).</span><span class="sxs-lookup"><span data-stu-id="8d22b-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="8d22b-212">д.</span><span class="sxs-lookup"><span data-stu-id="8d22b-212">e.</span></span>  <span data-ttu-id="8d22b-213">Щелкните **Сохранить конфигурацию**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="8d22b-214">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8d22b-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d22b-215">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8d22b-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d22b-216">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8d22b-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d22b-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d22b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d22b-218">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d22b-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8d22b-220">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8d22b-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d22b-221">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d22b-223">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d22b-225">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d22b-227">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8d22b-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d22b-229">а.</span><span class="sxs-lookup"><span data-stu-id="8d22b-229">a.</span></span> <span data-ttu-id="8d22b-230">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d22b-231">b.</span><span class="sxs-lookup"><span data-stu-id="8d22b-231">b.</span></span> <span data-ttu-id="8d22b-232">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d22b-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d22b-233">c.</span><span class="sxs-lookup"><span data-stu-id="8d22b-233">c.</span></span> <span data-ttu-id="8d22b-234">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d22b-235">d.</span><span class="sxs-lookup"><span data-stu-id="8d22b-235">d.</span></span> <span data-ttu-id="8d22b-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="8d22b-237">Создание тестового пользователя Slack</span><span class="sxs-lookup"><span data-stu-id="8d22b-237">Creating a Slack test user</span></span>

<span data-ttu-id="8d22b-238">Цель этого раздела — создать в Slack пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d22b-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="8d22b-239">Приложение Slack поддерживает JIT подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8d22b-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8d22b-240">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="8d22b-240">There is no action item for you in this section.</span></span> <span data-ttu-id="8d22b-241">Пользователь будет создан при попытке получить доступ к приложению Slack (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="8d22b-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="8d22b-242">Чтобы создать пользователя вручную, обратитесь к [группе поддержки Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="8d22b-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d22b-243">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d22b-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d22b-244">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8d22b-246">**Чтобы назначить пользователя Britta Simon в Slack, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8d22b-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="8d22b-247">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8d22b-249">В списке приложений выберите **Slack**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-249">In the applications list, select **Slack**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="8d22b-251">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8d22b-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-253">Click **Add** button.</span></span> <span data-ttu-id="8d22b-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8d22b-256">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d22b-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d22b-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8d22b-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d22b-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8d22b-259">Testing single sign-on</span></span>

<span data-ttu-id="8d22b-260">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8d22b-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d22b-261">Щелкнув плитку Slack на панели доступа, вы автоматически войдете в приложение Slack.</span><span class="sxs-lookup"><span data-stu-id="8d22b-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d22b-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8d22b-262">Additional resources</span></span>

* [<span data-ttu-id="8d22b-263">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d22b-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d22b-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d22b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

