---
title: "Руководство. Интеграция Azure Active Directory с Workpath | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="ead59-103">Руководство. Интеграция Azure Active Directory с Workpath</span><span class="sxs-lookup"><span data-stu-id="ead59-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="ead59-104">В этом руководстве описано, как интегрировать Workpath с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ead59-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ead59-105">Интеграция приложения Workpath с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ead59-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ead59-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="ead59-107">Вы можете включить автоматический вход пользователей в Workpath (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead59-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ead59-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ead59-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ead59-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ead59-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ead59-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ead59-110">Prerequisites</span></span>

<span data-ttu-id="ead59-111">Чтобы настроить интеграцию Azure AD с Workpath, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ead59-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="ead59-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ead59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ead59-113">подписка Workpath с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ead59-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ead59-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ead59-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ead59-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ead59-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ead59-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ead59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ead59-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ead59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ead59-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ead59-118">Scenario description</span></span>
<span data-ttu-id="ead59-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ead59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ead59-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ead59-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ead59-121">Добавление Workpath из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ead59-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="ead59-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="ead59-123">Добавление Workpath из коллекции</span><span class="sxs-lookup"><span data-stu-id="ead59-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="ead59-124">Чтобы настроить интеграцию приложения Workpath с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ead59-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ead59-125">**Добавление приложения Workpath из коллекции**</span><span class="sxs-lookup"><span data-stu-id="ead59-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ead59-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ead59-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ead59-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ead59-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ead59-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ead59-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ead59-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ead59-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ead59-133">В поле поиска введите **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="ead59-133">In the search box, type **Workpath**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="ead59-135">На панели результатов выберите **Workpath** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="ead59-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ead59-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ead59-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Workpath с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead59-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ead59-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в Workpath соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead59-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="ead59-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="ead59-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ead59-142">Чтобы настроить и проверить единый вход Azure AD в Workpath, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ead59-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ead59-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ead59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ead59-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ead59-145">**[Создание тестового пользователя Workpath](#creating-a-workpath-test-user)** требуется для создания в Workpath пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead59-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ead59-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead59-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ead59-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ead59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ead59-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ead59-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="ead59-150">**Настройка единого входа Azure AD в Workpath**</span><span class="sxs-lookup"><span data-stu-id="ead59-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="ead59-151">На портале Azure на странице интеграции с приложением **Workpath** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ead59-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ead59-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ead59-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="ead59-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Workpath** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ead59-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="ead59-157">а.</span><span class="sxs-lookup"><span data-stu-id="ead59-157">a.</span></span> <span data-ttu-id="ead59-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ead59-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="ead59-159">b.</span><span class="sxs-lookup"><span data-stu-id="ead59-159">b.</span></span> <span data-ttu-id="ead59-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://api.workpath.com/v1/saml/assert/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="ead59-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="ead59-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="ead59-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ead59-162">Если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ead59-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="ead59-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="ead59-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ead59-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ead59-165">These values are not real.</span></span> <span data-ttu-id="ead59-166">Укажите вместо них фактические значения URL-адреса для входа, идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="ead59-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="ead59-167">Обратитесь в [службу поддержки Workpath](https://help.workpath.com), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="ead59-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="ead59-168">Приложение Workpath ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="ead59-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ead59-169">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ead59-169">Configure the following claims for this application.</span></span> <span data-ttu-id="ead59-170">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="ead59-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ead59-171">На следующем снимке экрана приведен пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ead59-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="ead59-173">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ead59-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ead59-174">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ead59-174">Attribute Name</span></span> | <span data-ttu-id="ead59-175">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ead59-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ead59-176">first_name</span><span class="sxs-lookup"><span data-stu-id="ead59-176">first_name</span></span> | <span data-ttu-id="ead59-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ead59-177">user.givenname</span></span> |
    | <span data-ttu-id="ead59-178">last_name</span><span class="sxs-lookup"><span data-stu-id="ead59-178">last_name</span></span> | <span data-ttu-id="ead59-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="ead59-179">user.surname</span></span> |
    
    <span data-ttu-id="ead59-180">а.</span><span class="sxs-lookup"><span data-stu-id="ead59-180">a.</span></span> <span data-ttu-id="ead59-181">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="ead59-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ead59-183">b.</span><span class="sxs-lookup"><span data-stu-id="ead59-183">b.</span></span> <span data-ttu-id="ead59-184">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ead59-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ead59-186">c.</span><span class="sxs-lookup"><span data-stu-id="ead59-186">c.</span></span> <span data-ttu-id="ead59-187">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ead59-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ead59-188">г)</span><span class="sxs-lookup"><span data-stu-id="ead59-188">d.</span></span> <span data-ttu-id="ead59-189">Оставьте пустым текстовое поле **Пространство имен**.</span><span class="sxs-lookup"><span data-stu-id="ead59-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="ead59-190">д.</span><span class="sxs-lookup"><span data-stu-id="ead59-190">e.</span></span> <span data-ttu-id="ead59-191">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ead59-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="ead59-192">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ead59-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="ead59-194">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ead59-194">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="ead59-196">В разделе **Настройка Workpath** щелкните **Настроить Workpath**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ead59-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ead59-197">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ead59-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="ead59-199">Чтобы настроить единый вход на стороне **Workpath**, нужно отправить скачанный **XML-файл метаданных**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="ead59-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ead59-200">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ead59-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ead59-201">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ead59-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ead59-202">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ead59-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ead59-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead59-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="ead59-204">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead59-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ead59-206">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ead59-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ead59-207">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ead59-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ead59-209">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ead59-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ead59-211">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ead59-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ead59-213">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ead59-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ead59-215">а.</span><span class="sxs-lookup"><span data-stu-id="ead59-215">a.</span></span> <span data-ttu-id="ead59-216">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ead59-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ead59-217">b.</span><span class="sxs-lookup"><span data-stu-id="ead59-217">b.</span></span> <span data-ttu-id="ead59-218">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ead59-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ead59-219">c.</span><span class="sxs-lookup"><span data-stu-id="ead59-219">c.</span></span> <span data-ttu-id="ead59-220">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ead59-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ead59-221">d.</span><span class="sxs-lookup"><span data-stu-id="ead59-221">d.</span></span> <span data-ttu-id="ead59-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ead59-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="ead59-223">Создание тестового пользователя Workpath</span><span class="sxs-lookup"><span data-stu-id="ead59-223">Creating a Workpath test user</span></span>

<span data-ttu-id="ead59-224">Workpath поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="ead59-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="ead59-225">Пользователи создаются в приложении автоматически сразу после проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ead59-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ead59-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead59-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ead59-227">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ead59-229">**Назначение пользователя Britta Simon приложению Workpath**</span><span class="sxs-lookup"><span data-stu-id="ead59-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="ead59-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ead59-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ead59-232">В списке приложений выберите **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="ead59-232">In the applications list, select **Workpath**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="ead59-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ead59-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ead59-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ead59-236">Click **Add** button.</span></span> <span data-ttu-id="ead59-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ead59-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ead59-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ead59-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ead59-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ead59-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ead59-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ead59-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ead59-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ead59-242">Testing single sign-on</span></span>

<span data-ttu-id="ead59-243">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ead59-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ead59-244">Щелкнув плитку Workpath на панели доступа, вы автоматически войдете в приложение Workpath.</span><span class="sxs-lookup"><span data-stu-id="ead59-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="ead59-245">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ead59-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ead59-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ead59-246">Additional resources</span></span>

* [<span data-ttu-id="ead59-247">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ead59-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ead59-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ead59-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

