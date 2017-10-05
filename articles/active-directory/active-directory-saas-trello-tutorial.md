---
title: "Руководство по интеграции Azure Active Directory с Trello | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="fb880-103">Руководство. Интеграция Azure Active Directory с Trello</span><span class="sxs-lookup"><span data-stu-id="fb880-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="fb880-104">В этом руководстве описано, как интегрировать приложение Trello с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb880-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb880-105">Интеграция Azure AD с приложением Trello обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="fb880-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fb880-106">С помощью Azure AD вы можете контролировать доступ к Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="fb880-107">Вы можете включить автоматический вход пользователей в Trello (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb880-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb880-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fb880-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fb880-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb880-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb880-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb880-110">Prerequisites</span></span>

<span data-ttu-id="fb880-111">Чтобы настроить интеграцию Azure AD с Trello, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="fb880-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="fb880-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="fb880-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb880-113">подписка Trello с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="fb880-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb880-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="fb880-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb880-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="fb880-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb880-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fb880-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb880-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb880-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb880-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fb880-118">Scenario description</span></span>
<span data-ttu-id="fb880-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="fb880-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb880-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="fb880-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb880-121">Добавление Trello из коллекции</span><span class="sxs-lookup"><span data-stu-id="fb880-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="fb880-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb880-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="fb880-123">Добавление Trello из коллекции</span><span class="sxs-lookup"><span data-stu-id="fb880-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="fb880-124">Чтобы настроить интеграцию Trello с Azure AD, необходимо добавить Trello из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="fb880-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb880-125">**Чтобы добавить Trello из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fb880-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb880-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb880-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb880-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb880-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fb880-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb880-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="fb880-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="fb880-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="fb880-133">В поле поиска введите **Trello**.</span><span class="sxs-lookup"><span data-stu-id="fb880-133">In the search box, type **Trello**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="fb880-135">На панели результатов выберите **Trello** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="fb880-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb880-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb880-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb880-138">В этом разделе описана настройка и проверка единого входа Azure AD в Trello с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb880-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb880-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Trello соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb880-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="fb880-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="fb880-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fb880-142">Чтобы настроить и проверить единый вход Azure AD в Trello, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="fb880-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="fb880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fb880-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb880-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb880-145">**[Создание тестового пользователя Trello](#creating-a-trello-test-user)** требуется для того, чтобы в Trello существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb880-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb880-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb880-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb880-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fb880-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb880-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb880-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb880-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="fb880-150">**Чтобы настроить единый вход Azure AD в Trello, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fb880-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="fb880-151">На портале Azure на странице интеграции с приложением **Trello** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="fb880-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="fb880-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="fb880-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="fb880-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения Trello** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fb880-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="fb880-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://trello.com/auth/saml/consume/<enterprise>`.</span><span class="sxs-lookup"><span data-stu-id="fb880-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="fb880-158">Если вы хотите настроить приложение в **режиме, инициируемом поставщиком услуг**, то в разделе **Домены и URL-адреса приложения Trello** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fb880-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="fb880-160">а.</span><span class="sxs-lookup"><span data-stu-id="fb880-160">a.</span></span> <span data-ttu-id="fb880-161">Установите флажок **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="fb880-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="fb880-162">b.</span><span class="sxs-lookup"><span data-stu-id="fb880-162">b.</span></span> <span data-ttu-id="fb880-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://trello.com/auth/saml/consume/<enterprise>`.</span><span class="sxs-lookup"><span data-stu-id="fb880-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="fb880-164">Необходимо получить поле динамических данных **\<enterprise\>** из Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="fb880-165">При отсутствии значения поля динамических данных обратитесь к [группе поддержки Trello](mailto:support@trello.com), чтобы получить его для своего предприятия.</span><span class="sxs-lookup"><span data-stu-id="fb880-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="fb880-166">Приложение Trello ожидает, что утверждения SAML должны содержать определенные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="fb880-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="fb880-167">Настройте приведенные ниже атрибуты для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="fb880-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="fb880-168">Управлять значениями этих атрибутов можно на вкладке **Атрибуты пользователя** приложения.</span><span class="sxs-lookup"><span data-stu-id="fb880-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="fb880-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="fb880-169">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="fb880-171">В диалоговом окне **Атрибуты токена SAML** для каждой строки в таблице ниже выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fb880-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="fb880-172">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="fb880-172">Attribute Name</span></span> | <span data-ttu-id="fb880-173">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="fb880-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="fb880-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="fb880-174">User.Email</span></span> | <span data-ttu-id="fb880-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="fb880-175">user.mail</span></span> |
    | <span data-ttu-id="fb880-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="fb880-176">User.FirstName</span></span> | <span data-ttu-id="fb880-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="fb880-177">user.givenname</span></span> |
    | <span data-ttu-id="fb880-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="fb880-178">User.LastName</span></span> | <span data-ttu-id="fb880-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="fb880-179">user.surname</span></span> |

    <span data-ttu-id="fb880-180">а.</span><span class="sxs-lookup"><span data-stu-id="fb880-180">a.</span></span> <span data-ttu-id="fb880-181">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="fb880-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="fb880-184">b.</span><span class="sxs-lookup"><span data-stu-id="fb880-184">b.</span></span> <span data-ttu-id="fb880-185">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="fb880-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="fb880-186">c.</span><span class="sxs-lookup"><span data-stu-id="fb880-186">c.</span></span> <span data-ttu-id="fb880-187">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="fb880-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fb880-188">г)</span><span class="sxs-lookup"><span data-stu-id="fb880-188">d.</span></span> <span data-ttu-id="fb880-189">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb880-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="fb880-190">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="fb880-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="fb880-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="fb880-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb880-194">В разделе **Конфигурация Trello** щелкните **Настроить Trello**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="fb880-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fb880-195">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="fb880-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="fb880-197">Для настойки единого входа для приложения перейдите на страницу [Trello enterprise SSO configuration](https://trello.com/sso-configuration) (Конфигурация единого входа для предприятия Trello), чтобы отправить [группе поддержки Trello](mailto:support@trello.com) значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) и прикрепить скачанный **сертификат в кодировке Base64**.</span><span class="sxs-lookup"><span data-stu-id="fb880-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="fb880-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="fb880-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fb880-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="fb880-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fb880-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="fb880-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb880-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb880-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb880-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb880-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="fb880-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="fb880-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb880-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb880-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb880-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="fb880-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb880-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fb880-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb880-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fb880-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb880-213">а.</span><span class="sxs-lookup"><span data-stu-id="fb880-213">a.</span></span> <span data-ttu-id="fb880-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb880-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb880-215">b.</span><span class="sxs-lookup"><span data-stu-id="fb880-215">b.</span></span> <span data-ttu-id="fb880-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb880-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb880-217">c.</span><span class="sxs-lookup"><span data-stu-id="fb880-217">c.</span></span> <span data-ttu-id="fb880-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="fb880-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fb880-219">d.</span><span class="sxs-lookup"><span data-stu-id="fb880-219">d.</span></span> <span data-ttu-id="fb880-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb880-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="fb880-221">Создание тестового пользователя приложения Trello</span><span class="sxs-lookup"><span data-stu-id="fb880-221">Creating a Trello test user</span></span>

<span data-ttu-id="fb880-222">В этом разделе описано, как создать пользователя Britta Simon в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="fb880-223">В этом разделе описано, как создать пользователя Britta Simon в приложении Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="fb880-224">Trello поддерживает JIT-подготовку. При первом входе из Azure AD будет создана учетная запись.</span><span class="sxs-lookup"><span data-stu-id="fb880-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fb880-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb880-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fb880-226">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="fb880-228">**Чтобы назначить пользователя Britta Simon в Trello, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fb880-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="fb880-229">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb880-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="fb880-231">В списке приложений выберите **Trello**.</span><span class="sxs-lookup"><span data-stu-id="fb880-231">In the applications list, select **Trello**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="fb880-233">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fb880-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="fb880-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fb880-235">Click **Add** button.</span></span> <span data-ttu-id="fb880-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fb880-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="fb880-238">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fb880-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fb880-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fb880-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb880-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="fb880-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb880-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="fb880-241">Testing single sign-on</span></span>

<span data-ttu-id="fb880-242">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fb880-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="fb880-243">Щелкнув плитку Trello на панели доступа, вы автоматически войдете в приложение Trello.</span><span class="sxs-lookup"><span data-stu-id="fb880-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb880-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fb880-244">Additional resources</span></span>

* [<span data-ttu-id="fb880-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb880-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb880-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb880-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

