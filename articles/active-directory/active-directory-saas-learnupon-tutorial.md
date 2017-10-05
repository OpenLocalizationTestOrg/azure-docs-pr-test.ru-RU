---
title: "Руководство по интеграции Azure Active Directory с LearnUpon | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="e783a-103">Руководство. Интеграция Azure Active Directory с LearnUpon</span><span class="sxs-lookup"><span data-stu-id="e783a-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="e783a-104">В этом руководстве описано, как интегрировать LearnUpon с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e783a-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e783a-105">Интеграция Azure AD с приложением LearnUpon обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e783a-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e783a-106">С помощью Azure AD вы можете контролировать доступ к LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="e783a-107">Вы можете включить автоматический вход пользователей в LearnUpon (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e783a-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e783a-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e783a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e783a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e783a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e783a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e783a-110">Prerequisites</span></span>

<span data-ttu-id="e783a-111">Чтобы настроить интеграцию Azure AD с LearnUpon, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e783a-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="e783a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e783a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e783a-113">подписка LearnUpon с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e783a-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e783a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e783a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e783a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e783a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e783a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e783a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e783a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e783a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e783a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e783a-118">Scenario description</span></span>
<span data-ttu-id="e783a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e783a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e783a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e783a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e783a-121">Добавление LearnUpon из коллекции</span><span class="sxs-lookup"><span data-stu-id="e783a-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="e783a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e783a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="e783a-123">Добавление LearnUpon из коллекции</span><span class="sxs-lookup"><span data-stu-id="e783a-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="e783a-124">Чтобы настроить интеграцию LearnUpon с Azure AD, необходимо добавить LearnUpon из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e783a-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e783a-125">**Чтобы добавить LearnUpon из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e783a-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e783a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e783a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e783a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e783a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e783a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e783a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e783a-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e783a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e783a-133">В поле поиска введите **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="e783a-133">In the search box, type **LearnUpon**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="e783a-135">На панели результатов выберите **LearnUpon** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e783a-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e783a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e783a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e783a-138">В этом разделе описана настройка и проверка единого входа Azure AD в LearnUpon для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e783a-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e783a-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в LearnUpon соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e783a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="e783a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="e783a-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e783a-142">Чтобы настроить и проверить единый вход Azure AD в LearnUpon, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e783a-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e783a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e783a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e783a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e783a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e783a-145">**[Создание тестового пользователя LearnUpon](#creating-a-learnupon-test-user)** требуется для создания в LearnUpon пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e783a-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e783a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e783a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e783a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e783a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e783a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e783a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e783a-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="e783a-150">**Чтобы настроить единый вход Azure AD в LearnUpon, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e783a-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="e783a-151">На портале Azure на странице интеграции с приложением **LearnUpon** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e783a-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e783a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e783a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="e783a-155">В разделе **Домены и URL-адреса LearnUpon** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e783a-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="e783a-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.learnupon.com/saml/consumer`.</span><span class="sxs-lookup"><span data-stu-id="e783a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e783a-158">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e783a-158">Please note that this is not the real value.</span></span> <span data-ttu-id="e783a-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="e783a-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="e783a-160">Чтобы получить это значение, обратитесь в [службу поддержки LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="e783a-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="e783a-161">В разделе **Сертификат подписи SAML** щелкните **Certificate (Raw)** (Сертификат (необработанный)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e783a-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="e783a-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e783a-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e783a-165">В разделе **Настройка LearnUpon** щелкните **Настроить LearnUpon**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e783a-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e783a-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e783a-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="e783a-168">Откройте другую страницу браузера и войдите в LearnUpon с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="e783a-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="e783a-169">Перейдите на вкладку **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="e783a-169">Click the **settings** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="e783a-171">Щелкните **Single Sign On - SAML** (Единый вход — SAML), а затем нажмите кнопку **General Settings** (Общие параметры) для настройки SAML.</span><span class="sxs-lookup"><span data-stu-id="e783a-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="e783a-173">В разделе **General Settings** (Общие параметры) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e783a-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="e783a-175">а.</span><span class="sxs-lookup"><span data-stu-id="e783a-175">a.</span></span> <span data-ttu-id="e783a-176">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="e783a-176">Select **Enabled**.</span></span>

    <span data-ttu-id="e783a-177">b.</span><span class="sxs-lookup"><span data-stu-id="e783a-177">b.</span></span> <span data-ttu-id="e783a-178">Для параметра **Версия** установите значение **2.0**.</span><span class="sxs-lookup"><span data-stu-id="e783a-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="e783a-179">c.</span><span class="sxs-lookup"><span data-stu-id="e783a-179">c.</span></span> <span data-ttu-id="e783a-180">Для параметра **Пропустить условия** установите значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="e783a-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="e783a-181">г)</span><span class="sxs-lookup"><span data-stu-id="e783a-181">d.</span></span> <span data-ttu-id="e783a-182">В текстовое поле **SAML Token Post param name** (Имя параметра POST для токена SAML) введите имя параметра POST, передаваемого в запросе на указанный выше URL-адрес клиента SAML (в нем содержится требующее проверки и аутентификации утверждение SAML, например **SAMLResponse**).</span><span class="sxs-lookup"><span data-stu-id="e783a-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="e783a-183">д.</span><span class="sxs-lookup"><span data-stu-id="e783a-183">e.</span></span> <span data-ttu-id="e783a-184">В текстовое поле **Name Identifier Format** (Формат идентификатора имени) введите значение, которое определяет позицию идентификатора пользователя (адрес электронной почты) в утверждении SAML (например, **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**).</span><span class="sxs-lookup"><span data-stu-id="e783a-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="e783a-185">f.</span><span class="sxs-lookup"><span data-stu-id="e783a-185">f.</span></span> <span data-ttu-id="e783a-186">В текстовом поле **Расположение поставщика удостоверений** введите значение, которое определяет адрес, на который перенаправляются пользователи при щелчке по значку отправки на экране входа портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e783a-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="e783a-187">ж.</span><span class="sxs-lookup"><span data-stu-id="e783a-187">g.</span></span> <span data-ttu-id="e783a-188">В текстовом поле **URL-адрес выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e783a-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="e783a-189">h.</span><span class="sxs-lookup"><span data-stu-id="e783a-189">h.</span></span> <span data-ttu-id="e783a-190">Щелкните **Manage finger prints**(Управление отпечатками) и отправьте отпечаток загруженного сертификата.</span><span class="sxs-lookup"><span data-stu-id="e783a-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="e783a-191">Перейдите в раздел **User Settings**(Параметры пользователя) и выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="e783a-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="e783a-193">а.</span><span class="sxs-lookup"><span data-stu-id="e783a-193">a.</span></span> <span data-ttu-id="e783a-194">В текстовом поле **Формат идентификатора имени** введите значение, которое обозначает расположение имени пользователя в утверждении SAML, например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="e783a-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="e783a-195">b.</span><span class="sxs-lookup"><span data-stu-id="e783a-195">b.</span></span> <span data-ttu-id="e783a-196">В текстовом поле **Формат идентификатора фамилии** введите значение, которое обозначает расположение фамилии пользователя в утверждении SAML, например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="e783a-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="e783a-197">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e783a-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e783a-198">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e783a-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e783a-199">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e783a-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e783a-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e783a-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="e783a-201">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e783a-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e783a-203">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e783a-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e783a-204">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e783a-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e783a-206">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e783a-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e783a-208">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e783a-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e783a-210">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e783a-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e783a-212">а.</span><span class="sxs-lookup"><span data-stu-id="e783a-212">a.</span></span> <span data-ttu-id="e783a-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e783a-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e783a-214">b.</span><span class="sxs-lookup"><span data-stu-id="e783a-214">b.</span></span> <span data-ttu-id="e783a-215">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e783a-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e783a-216">c.</span><span class="sxs-lookup"><span data-stu-id="e783a-216">c.</span></span> <span data-ttu-id="e783a-217">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e783a-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e783a-218">d.</span><span class="sxs-lookup"><span data-stu-id="e783a-218">d.</span></span> <span data-ttu-id="e783a-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e783a-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="e783a-220">Создание тестового пользователя LearnUpon</span><span class="sxs-lookup"><span data-stu-id="e783a-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="e783a-221">Цель этого раздела — создать пользователя с именем Britta Simon в LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="e783a-222">Приложение LearnUpon поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e783a-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e783a-223">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="e783a-223">There is no action item for you in this section.</span></span> <span data-ttu-id="e783a-224">Пользователь будет создан при попытке получить доступ к приложению LearnUpon (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="e783a-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="e783a-225">[Настройка единого входа в Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e783a-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="e783a-226">Если вам нужно создать пользователя вручную, обратитесь в [службу поддержки LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="e783a-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e783a-227">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e783a-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e783a-228">В этом разделе описано, как включить единый вход для пользователя Britta Simon, предоставив этому пользователю доступ к LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e783a-230">**Чтобы назначить пользователя Britta Simon в LearnUpon, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e783a-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="e783a-231">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e783a-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e783a-233">В списке приложений выберите **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="e783a-233">In the applications list, select **LearnUpon**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="e783a-235">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e783a-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e783a-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e783a-237">Click **Add** button.</span></span> <span data-ttu-id="e783a-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e783a-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e783a-240">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e783a-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e783a-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e783a-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e783a-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e783a-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e783a-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e783a-243">Testing single sign-on</span></span>

<span data-ttu-id="e783a-244">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e783a-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e783a-245">Щелкнув элемент LearnUpon на панели доступа, вы автоматически войдете в приложение LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="e783a-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="e783a-246">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e783a-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e783a-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e783a-247">Additional resources</span></span>

* [<span data-ttu-id="e783a-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e783a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e783a-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e783a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

