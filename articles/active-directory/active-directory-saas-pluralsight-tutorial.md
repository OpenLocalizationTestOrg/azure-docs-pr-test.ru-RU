---
title: "Руководство по интеграции Azure Active Directory с Pluralsight | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="d0d17-103">Учебник. Интеграция Azure Active Directory с Pluralsight</span><span class="sxs-lookup"><span data-stu-id="d0d17-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="d0d17-104">В этом руководстве описано, как интегрировать Pluralsight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0d17-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0d17-105">Интеграция Pluralsight с Azure AD обеспечивает приведенные далее преимущества.</span><span class="sxs-lookup"><span data-stu-id="d0d17-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0d17-106">С помощью Azure AD вы можете контролировать доступ к Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="d0d17-107">Вы можете включить автоматический вход пользователей в Pluralsight (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d17-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0d17-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d17-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0d17-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0d17-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0d17-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d0d17-110">Prerequisites</span></span>

<span data-ttu-id="d0d17-111">Чтобы настроить интеграцию Azure AD с Pluralsight, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d0d17-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="d0d17-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d0d17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0d17-113">подписка Pluralsight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d0d17-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0d17-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d0d17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0d17-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d0d17-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0d17-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d0d17-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0d17-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0d17-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0d17-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d0d17-118">Scenario description</span></span>
<span data-ttu-id="d0d17-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d0d17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0d17-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d0d17-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0d17-121">Добавление Pluralsight из коллекции</span><span class="sxs-lookup"><span data-stu-id="d0d17-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="d0d17-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d17-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="d0d17-123">Добавление Pluralsight из коллекции</span><span class="sxs-lookup"><span data-stu-id="d0d17-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="d0d17-124">Чтобы настроить интеграцию Pluralsight с Azure AD, необходимо добавить Pluralsight из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0d17-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0d17-125">**Чтобы добавить Pluralsight из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d0d17-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d17-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0d17-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0d17-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d0d17-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d0d17-133">В поле поиска введите **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-133">In the search box, type **Pluralsight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="d0d17-135">На панели результатов выберите **Pluralsight** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d0d17-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0d17-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d17-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0d17-138">В этом разделе описана настройка и проверка единого входа Azure AD в Pluralsight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0d17-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0d17-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Pluralsight соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d17-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="d0d17-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="d0d17-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0d17-142">Чтобы настроить и проверить единый вход Azure AD в Pluralsight, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="d0d17-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0d17-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d0d17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0d17-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0d17-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0d17-145">**[Создание тестового пользователя Pluralsight](#creating-a-pluralsight-test-user)** требуется для того, чтобы в Pluralsight существовал пользователь Britta Simon, связанный с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d17-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0d17-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d17-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0d17-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0d17-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0d17-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d17-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0d17-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="d0d17-150">**Чтобы настроить единый вход Azure AD в Pluralsight, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d0d17-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d17-151">На портале Azure на странице интеграции с приложением **Pluralsight** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d0d17-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d0d17-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="d0d17-155">В разделе **Домены и URL-адреса приложения Pluralsight** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d0d17-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="d0d17-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="d0d17-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0d17-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="d0d17-158">This value is not real.</span></span> <span data-ttu-id="d0d17-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="d0d17-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d0d17-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов Pluralsight](mailto:support@pluralsight.com).</span><span class="sxs-lookup"><span data-stu-id="d0d17-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="d0d17-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d0d17-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="d0d17-163">В этом разделе описано, как включить единый вход Azure AD на портале Azure AD и настроить единый вход в приложении Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="d0d17-164">Для приложения Pluralsight проверочные утверждения SAML должны иметь определенный формат. Для этого необходимо добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов маркера SAML.</span><span class="sxs-lookup"><span data-stu-id="d0d17-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="d0d17-165">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="d0d17-165">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="d0d17-167">Также можно добавить атрибут **Уникальный идентификатор** с соответствующим значением, таким как EmployeeID или другим, которое подходит для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d0d17-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="d0d17-168">Обратите внимание, что это необязательный атрибут, однако его можно добавить для идентификации уникального пользователя.</span><span class="sxs-lookup"><span data-stu-id="d0d17-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="d0d17-169">Чтобы добавить требуемые **атрибуты маркера SAML**, для каждой строки в таблице ниже выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d0d17-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="d0d17-170">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="d0d17-170">Attribute Name</span></span> | <span data-ttu-id="d0d17-171">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="d0d17-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="d0d17-172">Имя</span><span class="sxs-lookup"><span data-stu-id="d0d17-172">First Name</span></span> |<span data-ttu-id="d0d17-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d0d17-173">user.givenname</span></span> |
   | <span data-ttu-id="d0d17-174">Фамилия</span><span class="sxs-lookup"><span data-stu-id="d0d17-174">Last Name</span></span> |<span data-ttu-id="d0d17-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="d0d17-175">user.surname</span></span> |
   | <span data-ttu-id="d0d17-176">Email</span><span class="sxs-lookup"><span data-stu-id="d0d17-176">Email</span></span> |<span data-ttu-id="d0d17-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="d0d17-177">user.mail</span></span> |
   
   <span data-ttu-id="d0d17-178">а.</span><span class="sxs-lookup"><span data-stu-id="d0d17-178">a.</span></span> <span data-ttu-id="d0d17-179">Щелкните **Добавить атрибут пользователя**, чтобы открыть диалоговое окно **Добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="d0d17-181">b.</span><span class="sxs-lookup"><span data-stu-id="d0d17-181">b.</span></span> <span data-ttu-id="d0d17-182">В текстовом поле **Имя атрибута** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d0d17-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="d0d17-183">c.</span><span class="sxs-lookup"><span data-stu-id="d0d17-183">c.</span></span> <span data-ttu-id="d0d17-184">В списке **Значение атрибута** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="d0d17-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="d0d17-185">г)</span><span class="sxs-lookup"><span data-stu-id="d0d17-185">d.</span></span> <span data-ttu-id="d0d17-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="d0d17-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d0d17-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d0d17-189">Чтобы настроить единый вход для своего приложения, свяжитесь с представителем отдела [профессиональных услуг](mailTo:professionalservices@pluralsight.com) Pluralsight и передайте ему скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="d0d17-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="d0d17-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d0d17-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0d17-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d0d17-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0d17-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d0d17-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0d17-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d17-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0d17-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0d17-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d0d17-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d0d17-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d17-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0d17-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0d17-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0d17-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d0d17-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0d17-205">а.</span><span class="sxs-lookup"><span data-stu-id="d0d17-205">a.</span></span> <span data-ttu-id="d0d17-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0d17-207">b.</span><span class="sxs-lookup"><span data-stu-id="d0d17-207">b.</span></span> <span data-ttu-id="d0d17-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0d17-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0d17-209">c.</span><span class="sxs-lookup"><span data-stu-id="d0d17-209">c.</span></span> <span data-ttu-id="d0d17-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0d17-211">d.</span><span class="sxs-lookup"><span data-stu-id="d0d17-211">d.</span></span> <span data-ttu-id="d0d17-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="d0d17-213">Создание тестового пользователя Pluralsight</span><span class="sxs-lookup"><span data-stu-id="d0d17-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="d0d17-214">Цель этого раздела — создать пользователя с именем Britta Simon в Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="d0d17-215">Чтобы добавить пользователей в учетную запись Pluralsight, обратитесь в [службу поддержки клиентов Pluralsight](mailto:support@pluralsight.com).</span><span class="sxs-lookup"><span data-stu-id="d0d17-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0d17-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0d17-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0d17-217">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Pluralsight, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d17-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d0d17-219">**Чтобы назначить пользователя Britta Simon в Pluralsight, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d0d17-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="d0d17-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d0d17-222">В списке приложений выберите **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-222">In the applications list, select **Pluralsight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="d0d17-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d0d17-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-226">Click **Add** button.</span></span> <span data-ttu-id="d0d17-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d0d17-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d0d17-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0d17-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d0d17-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0d17-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d0d17-232">Testing single sign-on</span></span>

<span data-ttu-id="d0d17-233">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d0d17-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0d17-234">Щелкнув элемент Pluralsight на панели доступа, вы автоматически войдете в приложение Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="d0d17-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="d0d17-235">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0d17-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0d17-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d0d17-236">Additional resources</span></span>

* [<span data-ttu-id="d0d17-237">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0d17-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0d17-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0d17-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

