---
title: "Руководство по интеграции Azure Active Directory с OfficeSpace Software | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="ed945-103">Учебник. Интеграция Azure Active Directory с OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="ed945-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="ed945-104">В этом руководстве описано, как интегрировать OfficeSpace Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed945-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed945-105">Интеграция OfficeSpace Software с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ed945-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed945-106">С помощью Azure AD вы можете контролировать доступ к OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="ed945-107">Вы можете включить автоматический вход пользователей в OfficeSpace Software (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed945-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ed945-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ed945-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ed945-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed945-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed945-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed945-110">Prerequisites</span></span>

<span data-ttu-id="ed945-111">Чтобы настроить интеграцию Azure AD с OfficeSpace Software, вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="ed945-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="ed945-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ed945-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed945-113">подписка OfficeSpace Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed945-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed945-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ed945-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed945-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ed945-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed945-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ed945-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed945-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed945-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed945-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ed945-118">Scenario description</span></span>
<span data-ttu-id="ed945-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ed945-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed945-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ed945-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed945-121">Добавление OfficeSpace Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="ed945-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="ed945-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed945-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="ed945-123">Добавление OfficeSpace Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="ed945-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="ed945-124">Чтобы настроить интеграцию OfficeSpace Software с Azure AD, необходимо добавить OfficeSpace Software из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed945-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed945-125">**Чтобы добавить OfficeSpace Software из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="ed945-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed945-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed945-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="ed945-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed945-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed945-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed945-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="ed945-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ed945-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="ed945-133">В поле поиска введите **OfficeSpace Software**, выберите **OfficeSpace Software** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ed945-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![OfficeSpace Software в списке результатов](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ed945-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed945-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ed945-136">В этом разделе описана настройка и проверка единого входа Azure AD в OfficeSpace Software с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed945-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed945-137">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в OfficeSpace Software соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed945-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="ed945-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="ed945-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed945-140">Чтобы настроить и проверить единый вход в Azure AD в OfficeSpace Software, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ed945-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed945-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ed945-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed945-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed945-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed945-143">**[Создание тестового пользователя OfficeSpace Software](#create-a-officespace-software-test-user)** требуется для создания в OfficeSpace Software пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed945-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed945-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed945-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed945-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed945-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ed945-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed945-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ed945-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="ed945-148">**Чтобы настроить единый вход Azure AD в OfficeSpace Software, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="ed945-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ed945-149">На портале Azure на странице интеграции с приложением **OfficeSpace Software** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ed945-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="ed945-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed945-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="ed945-153">В разделе **Домены и URL-адреса приложения OfficeSpace Software** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ed945-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="ed945-155">а.</span><span class="sxs-lookup"><span data-stu-id="ed945-155">a.</span></span> <span data-ttu-id="ed945-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="ed945-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="ed945-157">b.</span><span class="sxs-lookup"><span data-stu-id="ed945-157">b.</span></span> <span data-ttu-id="ed945-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="ed945-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed945-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ed945-159">These values are not real.</span></span> <span data-ttu-id="ed945-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ed945-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ed945-161">Обратитесь в [службу поддержки клиентов OfficeSpace Software](mailto:support@officespacesoftware.com), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="ed945-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="ed945-162">Приложение OfficeSpace Software ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="ed945-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ed945-163">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ed945-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="ed945-164">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="ed945-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ed945-165">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="ed945-165">The following screenshot shows an example for this.</span></span>
    
    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="ed945-167">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** выберите значение **user.mail** для параметра **Идентификатор пользователя**, а в каждой строке в таблице ниже выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ed945-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="ed945-168">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ed945-168">Attribute Name</span></span> | <span data-ttu-id="ed945-169">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ed945-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="ed945-170">email</span><span class="sxs-lookup"><span data-stu-id="ed945-170">email</span></span> | <span data-ttu-id="ed945-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="ed945-171">user.mail</span></span> |
    | <span data-ttu-id="ed945-172">name</span><span class="sxs-lookup"><span data-stu-id="ed945-172">name</span></span> | <span data-ttu-id="ed945-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="ed945-173">user.displayname</span></span> |
    | <span data-ttu-id="ed945-174">first_name</span><span class="sxs-lookup"><span data-stu-id="ed945-174">first_name</span></span> | <span data-ttu-id="ed945-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ed945-175">user.givenname</span></span> |
    | <span data-ttu-id="ed945-176">last_name</span><span class="sxs-lookup"><span data-stu-id="ed945-176">last_name</span></span> | <span data-ttu-id="ed945-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="ed945-177">user.surname</span></span> |

    <span data-ttu-id="ed945-178">а.</span><span class="sxs-lookup"><span data-stu-id="ed945-178">a.</span></span> <span data-ttu-id="ed945-179">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="ed945-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="ed945-180">Настройка при добавлении</span><span class="sxs-lookup"><span data-stu-id="ed945-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Настройка атрибута](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ed945-182">b.</span><span class="sxs-lookup"><span data-stu-id="ed945-182">b.</span></span> <span data-ttu-id="ed945-183">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ed945-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ed945-184">c.</span><span class="sxs-lookup"><span data-stu-id="ed945-184">c.</span></span> <span data-ttu-id="ed945-185">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ed945-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ed945-186">d.</span><span class="sxs-lookup"><span data-stu-id="ed945-186">d.</span></span> <span data-ttu-id="ed945-187">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ed945-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="ed945-188">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток** для сертификата.</span><span class="sxs-lookup"><span data-stu-id="ed945-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="ed945-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ed945-190">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ed945-192">В разделе **OfficeSpace Software Configuration** (Конфигурация OfficeSpace Software) щелкните **Configure OfficeSpace Software** (Настройка OfficeSpace Software), чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ed945-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ed945-193">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="ed945-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="ed945-195">В другом окне веб-браузера войдите в свой клиент OfficeSpace Software в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ed945-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="ed945-196">Выберите **Settings** (Параметры) и щелкните **Connectors** (Соединители).</span><span class="sxs-lookup"><span data-stu-id="ed945-196">Go to **Settings** and click **Connectors**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="ed945-198">Щелкните **SAML Authentication** (Аутентификация SAML).</span><span class="sxs-lookup"><span data-stu-id="ed945-198">Click **SAML Authentication**.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="ed945-200">В разделе **Проверка подлинности SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ed945-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="ed945-202">а.</span><span class="sxs-lookup"><span data-stu-id="ed945-202">a.</span></span> <span data-ttu-id="ed945-203">В текстовое поле **Logout provider url** (URL-адрес поставщика для выхода) вставьте значение **URL-адреса выхода**, скопированное с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed945-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ed945-204">b.</span><span class="sxs-lookup"><span data-stu-id="ed945-204">b.</span></span> <span data-ttu-id="ed945-205">В текстовое поле **Client idp target url** (Целевой URL-адрес IDP клиента) вставьте значение **URL-адреса службы единого входа SAML**, скопированное с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed945-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ed945-206">c.</span><span class="sxs-lookup"><span data-stu-id="ed945-206">c.</span></span> <span data-ttu-id="ed945-207">В текстовое поле **Client IDP certificate fingerprint** (Отпечаток сертификата IDP клиента) вставьте значение **отпечатка**, скопированное с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed945-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="ed945-208">d.</span><span class="sxs-lookup"><span data-stu-id="ed945-208">d.</span></span> <span data-ttu-id="ed945-209">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="ed945-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="ed945-210">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ed945-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed945-211">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ed945-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed945-212">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ed945-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ed945-213">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed945-213">Create an Azure AD test user</span></span>

<span data-ttu-id="ed945-214">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed945-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="ed945-216">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ed945-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed945-217">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed945-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ed945-219">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ed945-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ed945-221">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed945-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ed945-223">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ed945-223">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ed945-225">а.</span><span class="sxs-lookup"><span data-stu-id="ed945-225">a.</span></span> <span data-ttu-id="ed945-226">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed945-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed945-227">b.</span><span class="sxs-lookup"><span data-stu-id="ed945-227">b.</span></span> <span data-ttu-id="ed945-228">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed945-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ed945-229">c.</span><span class="sxs-lookup"><span data-stu-id="ed945-229">c.</span></span> <span data-ttu-id="ed945-230">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ed945-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ed945-231">г)</span><span class="sxs-lookup"><span data-stu-id="ed945-231">d.</span></span> <span data-ttu-id="ed945-232">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ed945-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="ed945-233">Создание тестового пользователя OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="ed945-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="ed945-234">Цель этого раздела — создать пользователя Britta Simon в OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="ed945-235">Приложение OfficeSpace Software поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ed945-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ed945-236">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="ed945-236">There is no action item for you in this section.</span></span> <span data-ttu-id="ed945-237">Пользователь будет создан при попытке получить доступ к OfficeSpace Software (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="ed945-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ed945-238">Чтобы создать пользователя вручную, необходимо обратиться к [группе поддержки OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="ed945-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ed945-239">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed945-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="ed945-240">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="ed945-242">**Чтобы назначить Britta Simon в OfficeSpace Software, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="ed945-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="ed945-243">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed945-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ed945-245">Из списка приложений выберите **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="ed945-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![Ссылка на OfficeSpace Software в списке "Приложения"](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="ed945-247">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed945-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="ed945-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed945-249">Click **Add** button.</span></span> <span data-ttu-id="ed945-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed945-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="ed945-252">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed945-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed945-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ed945-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed945-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ed945-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ed945-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ed945-255">Test single sign-on</span></span>

<span data-ttu-id="ed945-256">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ed945-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed945-257">Щелкнув элемент "OfficeSpace Software" на панели доступа, вы автоматически войдете в приложение OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="ed945-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed945-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ed945-258">Additional resources</span></span>

* [<span data-ttu-id="ed945-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed945-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed945-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed945-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

