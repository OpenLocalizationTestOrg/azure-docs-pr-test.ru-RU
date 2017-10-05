---
title: "Руководство по интеграции Azure Active Directory с Veracode | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="11db7-103">Руководство. Интеграция Azure Active Directory с Veracode</span><span class="sxs-lookup"><span data-stu-id="11db7-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="11db7-104">В этом руководстве описано, как интегрировать Veracode с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11db7-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11db7-105">Интеграция Veracode с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="11db7-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11db7-106">С помощью Azure AD вы можете контролировать доступ к Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="11db7-107">Вы можете включить автоматический вход пользователей в Veracode (единый вход) с учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11db7-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="11db7-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="11db7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="11db7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11db7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11db7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11db7-110">Prerequisites</span></span>

<span data-ttu-id="11db7-111">Чтобы настроить интеграцию Azure AD с приложением Veracode, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="11db7-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="11db7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="11db7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11db7-113">Подписка Veracode с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="11db7-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11db7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="11db7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11db7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="11db7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11db7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="11db7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11db7-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11db7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11db7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="11db7-118">Scenario description</span></span>
<span data-ttu-id="11db7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="11db7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11db7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="11db7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11db7-121">Добавление Veracode из коллекции</span><span class="sxs-lookup"><span data-stu-id="11db7-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="11db7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="11db7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="11db7-123">Добавление Veracode из коллекции</span><span class="sxs-lookup"><span data-stu-id="11db7-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="11db7-124">Чтобы настроить интеграцию Veracode с Azure AD, необходимо добавить Veracode из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="11db7-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11db7-125">**Чтобы добавить Veracode из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="11db7-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11db7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11db7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="11db7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="11db7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11db7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="11db7-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="11db7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="11db7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="11db7-133">В поле поиска введите **Veracode**, выберите **Veracode** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="11db7-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode в списке результатов](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="11db7-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="11db7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="11db7-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Veracode с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11db7-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11db7-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Veracode соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11db7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="11db7-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="11db7-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11db7-140">Чтобы настроить и проверить единый вход Azure AD в Veracode, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="11db7-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11db7-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="11db7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11db7-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11db7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11db7-143">**[Создание тестового пользователя Veracode](#create-a-veracode-test-user)** требуется для того, чтобы в Veracode существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11db7-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="11db7-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11db7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11db7-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="11db7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="11db7-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="11db7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="11db7-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="11db7-148">**Чтобы настроить единый вход Azure AD в Veracode, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="11db7-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="11db7-149">На портале Azure на странице интеграции с приложением **Veracode** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="11db7-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="11db7-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="11db7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="11db7-153">В разделе **Домен и URL-адреса единого входа в Veracode** не нужно выполнять никаких действий, так как приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="11db7-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="11db7-155">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="11db7-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="11db7-157">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Veracode с помощью своей учетной записи Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="11db7-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="11db7-158">Приложение Veracode ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию **атрибутов токена SAML** .</span><span class="sxs-lookup"><span data-stu-id="11db7-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="11db7-159">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="11db7-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="11db7-160">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="11db7-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="11db7-161">Чтобы добавить обязательные сопоставления атрибутов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11db7-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="11db7-162">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="11db7-162">Attribute Name</span></span> | <span data-ttu-id="11db7-163">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="11db7-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="11db7-164">firstname</span><span class="sxs-lookup"><span data-stu-id="11db7-164">firstname</span></span> |<span data-ttu-id="11db7-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="11db7-165">User.givenname</span></span> |
    | <span data-ttu-id="11db7-166">lastname</span><span class="sxs-lookup"><span data-stu-id="11db7-166">lastname</span></span> |<span data-ttu-id="11db7-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="11db7-167">User.surname</span></span> |
    | <span data-ttu-id="11db7-168">email</span><span class="sxs-lookup"><span data-stu-id="11db7-168">email</span></span> |<span data-ttu-id="11db7-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="11db7-169">User.mail</span></span> |
    
    <span data-ttu-id="11db7-170">а.</span><span class="sxs-lookup"><span data-stu-id="11db7-170">a.</span></span> <span data-ttu-id="11db7-171">Для каждой строки данных в приведенной выше таблице нажмите кнопку **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="11db7-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="11db7-172">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="11db7-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="11db7-173">![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="11db7-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="11db7-174">b.</span><span class="sxs-lookup"><span data-stu-id="11db7-174">b.</span></span> <span data-ttu-id="11db7-175">В текстовом поле **Имя атрибута** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="11db7-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="11db7-176">c.</span><span class="sxs-lookup"><span data-stu-id="11db7-176">c.</span></span> <span data-ttu-id="11db7-177">В текстовом поле **Значение атрибута** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="11db7-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="11db7-178">d.</span><span class="sxs-lookup"><span data-stu-id="11db7-178">d.</span></span> <span data-ttu-id="11db7-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="11db7-179">Click **Ok**.</span></span>

7. <span data-ttu-id="11db7-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="11db7-180">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="11db7-182">В разделе **Конфигурация Veracode** щелкните **Настроить Veracode**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="11db7-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="11db7-183">Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="11db7-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Конфигурация Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="11db7-185">В другом окне веб-браузера войдите на веб-сайт Veracode вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="11db7-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="11db7-186">В верхнем меню нажмите **Settings** (Параметры), а затем выберите **Admin** (Администратор).</span><span class="sxs-lookup"><span data-stu-id="11db7-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="11db7-187">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802911.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="11db7-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="11db7-188">Щелкните вкладку **SAML** .</span><span class="sxs-lookup"><span data-stu-id="11db7-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="11db7-189">В разделе **Параметры SAML для организации** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11db7-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="11db7-190">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802912.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="11db7-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="11db7-191">а.</span><span class="sxs-lookup"><span data-stu-id="11db7-191">a.</span></span>  <span data-ttu-id="11db7-192">В текстовое поле **Issuer** (Издатель) вставьте **идентификатор сущности SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="11db7-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="11db7-193">b.</span><span class="sxs-lookup"><span data-stu-id="11db7-193">b.</span></span> <span data-ttu-id="11db7-194">Чтобы загрузить сертификат, скачанный на портале Azure, нажмите кнопку **Choose File** (Выбрать файл).</span><span class="sxs-lookup"><span data-stu-id="11db7-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="11db7-195">c.</span><span class="sxs-lookup"><span data-stu-id="11db7-195">c.</span></span> <span data-ttu-id="11db7-196">Выберите параметр **Включить саморегистрацию**.</span><span class="sxs-lookup"><span data-stu-id="11db7-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="11db7-197">В разделе **Self Registration Settings** (Параметры саморегистрации) выполните следующие действия, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="11db7-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="11db7-198">![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802913.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="11db7-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="11db7-199">а.</span><span class="sxs-lookup"><span data-stu-id="11db7-199">a.</span></span> <span data-ttu-id="11db7-200">Для параметра **New User Activation** (Активация нового пользователя) выберите значение **No Activation Required** (Активация не требуется).</span><span class="sxs-lookup"><span data-stu-id="11db7-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="11db7-201">b.</span><span class="sxs-lookup"><span data-stu-id="11db7-201">b.</span></span> <span data-ttu-id="11db7-202">Для параметра **User Data Updates** (Обновления пользовательских данных) выберите значение **Preference Veracode User Data** (Предпочтение пользовательских данных Veracode).</span><span class="sxs-lookup"><span data-stu-id="11db7-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="11db7-203">c.</span><span class="sxs-lookup"><span data-stu-id="11db7-203">c.</span></span> <span data-ttu-id="11db7-204">Для параметра **Сведения об атрибутах SAML**выберите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="11db7-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="11db7-205">**роли пользователей;**</span><span class="sxs-lookup"><span data-stu-id="11db7-205">**User Roles**</span></span>
      * <span data-ttu-id="11db7-206">**администратор политики;**</span><span class="sxs-lookup"><span data-stu-id="11db7-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="11db7-207">**рецензент;**</span><span class="sxs-lookup"><span data-stu-id="11db7-207">**Reviewer**</span></span>
      * <span data-ttu-id="11db7-208">**руководитель безопасности;**</span><span class="sxs-lookup"><span data-stu-id="11db7-208">**Security Lead**</span></span>
      * <span data-ttu-id="11db7-209">**руководитель;**</span><span class="sxs-lookup"><span data-stu-id="11db7-209">**Executive**</span></span>
      * <span data-ttu-id="11db7-210">**отправитель;**</span><span class="sxs-lookup"><span data-stu-id="11db7-210">**Submitter**</span></span>
      * <span data-ttu-id="11db7-211">**создатель;**</span><span class="sxs-lookup"><span data-stu-id="11db7-211">**Creator**</span></span>
      * <span data-ttu-id="11db7-212">**все типы проверки;**</span><span class="sxs-lookup"><span data-stu-id="11db7-212">**All Scan Types**</span></span>
      * <span data-ttu-id="11db7-213">**участие в группе;**</span><span class="sxs-lookup"><span data-stu-id="11db7-213">**Team Memberships**</span></span>
      * <span data-ttu-id="11db7-214">**группа по умолчанию.**</span><span class="sxs-lookup"><span data-stu-id="11db7-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="11db7-215">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="11db7-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11db7-216">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="11db7-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11db7-217">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="11db7-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="11db7-218">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="11db7-218">Create an Azure AD test user</span></span>

<span data-ttu-id="11db7-219">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11db7-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="11db7-221">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="11db7-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11db7-222">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11db7-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="11db7-224">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="11db7-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="11db7-226">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="11db7-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="11db7-228">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="11db7-228">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="11db7-230">а.</span><span class="sxs-lookup"><span data-stu-id="11db7-230">a.</span></span> <span data-ttu-id="11db7-231">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11db7-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11db7-232">b.</span><span class="sxs-lookup"><span data-stu-id="11db7-232">b.</span></span> <span data-ttu-id="11db7-233">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11db7-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="11db7-234">c.</span><span class="sxs-lookup"><span data-stu-id="11db7-234">c.</span></span> <span data-ttu-id="11db7-235">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="11db7-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="11db7-236">г)</span><span class="sxs-lookup"><span data-stu-id="11db7-236">d.</span></span> <span data-ttu-id="11db7-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="11db7-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="11db7-238">Создание тестового пользователя Veracode</span><span class="sxs-lookup"><span data-stu-id="11db7-238">Create a Veracode test user</span></span>
<span data-ttu-id="11db7-239">Чтобы пользователи Azure AD могли выполнять вход в Veracode, они должны быть подготовлены для Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="11db7-240">В случае Veracode подготовка выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="11db7-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="11db7-241">С вашей стороны никакие действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="11db7-241">There is no action item for you.</span></span> <span data-ttu-id="11db7-242">В случае необходимости пользователи создаются автоматически при первой попытке входа в систему.</span><span class="sxs-lookup"><span data-stu-id="11db7-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="11db7-243">Вы можете использовать любые другие средства создания учетной записи пользователя Veracode или API-интерфейсы, предоставляемые Veracode для подготовки учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11db7-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="11db7-244">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="11db7-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="11db7-245">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="11db7-247">**Чтобы назначить пользователя Britta Simon в Veracode, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="11db7-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="11db7-248">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="11db7-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="11db7-250">В списке приложений выберите **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="11db7-250">In the applications list, select **Veracode**.</span></span>

    ![Ссылка на Veracode в списке "Приложения"](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="11db7-252">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="11db7-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="11db7-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="11db7-254">Click **Add** button.</span></span> <span data-ttu-id="11db7-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="11db7-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="11db7-257">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="11db7-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11db7-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="11db7-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11db7-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="11db7-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="11db7-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="11db7-260">Test single sign-on</span></span>

<span data-ttu-id="11db7-261">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="11db7-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11db7-262">Щелкнув плитку Veracode на панели доступа, вы автоматически войдете в приложение Veracode.</span><span class="sxs-lookup"><span data-stu-id="11db7-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="11db7-263">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11db7-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="11db7-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="11db7-264">Additional resources</span></span>

* [<span data-ttu-id="11db7-265">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11db7-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11db7-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11db7-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

