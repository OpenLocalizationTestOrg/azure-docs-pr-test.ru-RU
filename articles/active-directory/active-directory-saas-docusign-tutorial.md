---
title: "Учебник. Интеграция Azure Active Directory с DocuSign | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="808d0-103">Учебник. Интеграция Azure Active Directory с DocuSign</span><span class="sxs-lookup"><span data-stu-id="808d0-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="808d0-104">В этом руководстве описано, как интегрировать DocuSign с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="808d0-104">In this tutorial, you learn how to integrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="808d0-105">Интеграция Azure AD с приложением DocuSign обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="808d0-105">Integrating DocuSign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="808d0-106">С помощью Azure AD вы можете контролировать доступ к DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-106">You can control in Azure AD who has access to DocuSign</span></span>
- <span data-ttu-id="808d0-107">Вы можете включить автоматический вход пользователей в DocuSign (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-107">You can enable your users to automatically get signed-on to DocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="808d0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="808d0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="808d0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="808d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="808d0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="808d0-110">Prerequisites</span></span>

<span data-ttu-id="808d0-111">Чтобы настроить интеграцию Azure AD с DocuSign, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="808d0-111">To configure Azure AD integration with DocuSign, you need the following items:</span></span>

- <span data-ttu-id="808d0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="808d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="808d0-113">подписка DocuSign с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="808d0-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="808d0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="808d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="808d0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="808d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="808d0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="808d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="808d0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="808d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="808d0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="808d0-118">Scenario description</span></span>
<span data-ttu-id="808d0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="808d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="808d0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="808d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="808d0-121">Добавление DocuSign из коллекции</span><span class="sxs-lookup"><span data-stu-id="808d0-121">Adding DocuSign from the gallery</span></span>
2. <span data-ttu-id="808d0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="808d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-the-gallery"></a><span data-ttu-id="808d0-123">Добавление DocuSign из коллекции</span><span class="sxs-lookup"><span data-stu-id="808d0-123">Adding DocuSign from the gallery</span></span>
<span data-ttu-id="808d0-124">Чтобы настроить интеграцию DocuSign с Azure AD, необходимо добавить DocuSign из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="808d0-124">To configure the integration of DocuSign into Azure AD, you need to add DocuSign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="808d0-125">**Чтобы добавить DocuSign из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="808d0-125">**To add DocuSign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="808d0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="808d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="808d0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="808d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="808d0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="808d0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="808d0-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="808d0-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="808d0-133">В поле поиска введите **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="808d0-133">In the search box, type **DocuSign**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="808d0-135">На панели результатов выберите **DocuSign** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="808d0-135">In the results panel, select **DocuSign**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="808d0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="808d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="808d0-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение DocuSign с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="808d0-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="808d0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в DocuSign соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DocuSign is to a user in Azure AD.</span></span> <span data-ttu-id="808d0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-140">In other words, a link relationship between an Azure AD user and the related user in DocuSign needs to be established.</span></span>

<span data-ttu-id="808d0-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in DocuSign.</span></span>

<span data-ttu-id="808d0-142">Чтобы настроить и проверить единый вход Azure AD в DocuSign, вам потребуется выполнить действия в перечисленных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="808d0-142">To configure and test Azure AD single sign-on with DocuSign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="808d0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="808d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="808d0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="808d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="808d0-145">**[Создание тестового пользователя DocuSign](#creating-a-docusign-test-user)** требуется для создания в DocuSign пользователя Britta Simon, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - to have a counterpart of Britta Simon in DocuSign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="808d0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="808d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="808d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="808d0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="808d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="808d0-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="808d0-150">**Чтобы настроить единый вход Azure AD в DocuSign, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="808d0-150">**To configure Azure AD single sign-on with DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="808d0-151">На портале Azure на странице интеграции с приложением **DocuSign** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="808d0-151">In the Azure portal, on the **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="808d0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="808d0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="808d0-155">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="808d0-155">On the **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="808d0-157">В разделе **Настройка DocuSign** на портале Azure щелкните **Настроить DocuSign**, чтобы открыть окно "Настройка единого входа".</span><span class="sxs-lookup"><span data-stu-id="808d0-157">On the **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** to open Configure sign-on window.</span></span> <span data-ttu-id="808d0-158">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="808d0-158">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="808d0-160">В другом окне браузера войдите на **портал администрирования DocuSign** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="808d0-160">In a different web browser window, login to your **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="808d0-161">В меню навигации слева щелкните **Domains**(Домены).</span><span class="sxs-lookup"><span data-stu-id="808d0-161">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Настройка единого входа][51]

7. <span data-ttu-id="808d0-163">На правой панели щелкните **Claim Domain**(Зарезервировать домен).</span><span class="sxs-lookup"><span data-stu-id="808d0-163">On the right pane, click **Claim Domain**.</span></span>
   
    ![Настройка единого входа][52]

8. <span data-ttu-id="808d0-165">В диалоговом окне **Claim a domain** (Резервирование домена) в текстовом поле **Domain Name** (Доменное имя) введите соответствующее доменное имя своей компании и нажмите кнопку **Claim** (Зарезервировать).</span><span class="sxs-lookup"><span data-stu-id="808d0-165">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="808d0-166">Обязательно проверьте домен. Состояние домена должно быть "Активный".</span><span class="sxs-lookup"><span data-stu-id="808d0-166">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Настройка единого входа][53]

9. <span data-ttu-id="808d0-168">На панели навигации слева щелкните **Identity Providers**</span><span class="sxs-lookup"><span data-stu-id="808d0-168">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Настройка единого входа][54]
10. <span data-ttu-id="808d0-170">На панели справа нажмите кнопку **Add identity provider**(Добавить поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="808d0-170">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Настройка единого входа][55]

11. <span data-ttu-id="808d0-172">На странице **параметров поставщика удостоверений** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="808d0-172">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Настройка единого входа][56]

    <span data-ttu-id="808d0-174">а.</span><span class="sxs-lookup"><span data-stu-id="808d0-174">a.</span></span> <span data-ttu-id="808d0-175">В соответствующее текстовое поле введите уникальное **имя** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="808d0-175">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="808d0-176">Не используйте пробелы.</span><span class="sxs-lookup"><span data-stu-id="808d0-176">Do not use spaces.</span></span>

    <span data-ttu-id="808d0-177">b.</span><span class="sxs-lookup"><span data-stu-id="808d0-177">b.</span></span> <span data-ttu-id="808d0-178">Вставьте **идентификатор сущности SAML** в текстовом поле **Издатель поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="808d0-178">Paste **SAML Entity ID** into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="808d0-179">c.</span><span class="sxs-lookup"><span data-stu-id="808d0-179">c.</span></span> <span data-ttu-id="808d0-180">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **URL-адрес для входа поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="808d0-180">Paste **SAML Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="808d0-181">г)</span><span class="sxs-lookup"><span data-stu-id="808d0-181">d.</span></span> <span data-ttu-id="808d0-182">Вставьте **URL-адрес выхода** в текстовое поле **URL-адрес для выхода поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="808d0-182">Paste **Sign-Out URL** into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="808d0-183">д.</span><span class="sxs-lookup"><span data-stu-id="808d0-183">e.</span></span> <span data-ttu-id="808d0-184">Выберите **Sign AuthN Request**(Подпись запроса авторизации).</span><span class="sxs-lookup"><span data-stu-id="808d0-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="808d0-185">Е.</span><span class="sxs-lookup"><span data-stu-id="808d0-185">f.</span></span> <span data-ttu-id="808d0-186">Для параметра **Send AuthN request by** (Как отправлять запрос авторизации) выберите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="808d0-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="808d0-187">g.</span><span class="sxs-lookup"><span data-stu-id="808d0-187">g.</span></span> <span data-ttu-id="808d0-188">Для параметра **Send logout request by** (Как отправлять запрос на выход) выберите значение **GET**.</span><span class="sxs-lookup"><span data-stu-id="808d0-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="808d0-189">В разделе **Custom Attribute Mapping** (Сопоставление настраиваемого атрибута) выберите поле, которое нужно сопоставить с утверждением Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-189">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="808d0-190">Например, утверждение **emailaddress** сопоставляется со значением **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="808d0-190">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="808d0-191">Это имя утверждения по умолчанию из Azure AD, которое используется для утверждения на электронную почту.</span><span class="sxs-lookup"><span data-stu-id="808d0-191">It is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="808d0-192">Чтобы сопоставить пользователя Azure AD с пользователем Docusign, используйте соответствующий **идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="808d0-192">Use the appropriate **User identifier** to map the user from Azure AD to DocuSign user mapping.</span></span> <span data-ttu-id="808d0-193">Выберите соответствующее поле и введите подходящее значение на основе параметров вашей организации.</span><span class="sxs-lookup"><span data-stu-id="808d0-193">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
          
    ![Настройка единого входа][57]

13. <span data-ttu-id="808d0-195">В разделе **Identity Provider Certificate** (Сертификат поставщика удостоверений) нажмите кнопку **Add Certificate** (Добавить сертификат) и отправьте сертификат, который вы скачали на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="808d0-195">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Настройка единого входа][58]

14. <span data-ttu-id="808d0-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="808d0-197">Click **Save**.</span></span>

15. <span data-ttu-id="808d0-198">В разделе **Identity Providers** (Поставщики удостоверений) нажмите кнопку **Actions** (Действия), а затем выберите **Endpoints** (Конечные точки).</span><span class="sxs-lookup"><span data-stu-id="808d0-198">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Настройка единого входа][59]
 
16. <span data-ttu-id="808d0-200">На **портале администрирования DocuSign** в разделе **View SAML 2.0 Endpoints** (Просмотр конечных точек SAML 2.0) выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="808d0-200">In the **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform the following steps:</span></span>
   
    ![Настройка единого входа][60]
   
    <span data-ttu-id="808d0-202">а.</span><span class="sxs-lookup"><span data-stu-id="808d0-202">a.</span></span> <span data-ttu-id="808d0-203">Скопируйте значение **Service Provider Issuer URL** (URL-адрес издателя поставщика услуг), а затем вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения DocuSign** на портале Azure, используя следующий шаблон: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="808d0-203">Copy the **Service Provider Issuer URL**, and then paste into the **Identifier** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="808d0-204">b.</span><span class="sxs-lookup"><span data-stu-id="808d0-204">b.</span></span> <span data-ttu-id="808d0-205">Скопируйте значение **Service Provider Login URL** (URL-адрес для входа поставщика услуг), а затем вставьте его в текстовое поле **URL-адрес для входа** в разделе **Домены и URL-адреса приложения DocuSign** на портале Azure, используя следующий шаблон: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="808d0-205">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on **DocuSign Domain and URLs** section of the Azure portal following the pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="808d0-207">c.</span><span class="sxs-lookup"><span data-stu-id="808d0-207">c.</span></span>  <span data-ttu-id="808d0-208">В нижней части страницы нажмите кнопку **Close**</span><span class="sxs-lookup"><span data-stu-id="808d0-208">Click **Close**</span></span>
    
17. <span data-ttu-id="808d0-209">На портале Azure нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="808d0-209">On the Azure portal, click **Save**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="808d0-211">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="808d0-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="808d0-212">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="808d0-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="808d0-213">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="808d0-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="808d0-214">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="808d0-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="808d0-215">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="808d0-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="808d0-217">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="808d0-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="808d0-218">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="808d0-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="808d0-220">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="808d0-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="808d0-222">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="808d0-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="808d0-224">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="808d0-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="808d0-226">а.</span><span class="sxs-lookup"><span data-stu-id="808d0-226">a.</span></span> <span data-ttu-id="808d0-227">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="808d0-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="808d0-228">b.</span><span class="sxs-lookup"><span data-stu-id="808d0-228">b.</span></span> <span data-ttu-id="808d0-229">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="808d0-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="808d0-230">c.</span><span class="sxs-lookup"><span data-stu-id="808d0-230">c.</span></span> <span data-ttu-id="808d0-231">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="808d0-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="808d0-232">d.</span><span class="sxs-lookup"><span data-stu-id="808d0-232">d.</span></span> <span data-ttu-id="808d0-233">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="808d0-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="808d0-234">Создание тестового пользователя DocuSign</span><span class="sxs-lookup"><span data-stu-id="808d0-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="808d0-235">Приложение поддерживает **JIT-подготовку пользователей**, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="808d0-235">Application supports **Just in time user provisioning** and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="808d0-236">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="808d0-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="808d0-237">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-237">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to DocuSign.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="808d0-239">**Чтобы назначить пользователя Britta Simon в DocuSign, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="808d0-239">**To assign Britta Simon to DocuSign, perform the following steps:**</span></span>

1. <span data-ttu-id="808d0-240">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="808d0-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="808d0-242">В списке приложений выберите **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="808d0-242">In the applications list, select **DocuSign**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="808d0-244">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="808d0-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="808d0-246">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="808d0-246">Click **Add** button.</span></span> <span data-ttu-id="808d0-247">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="808d0-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="808d0-249">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="808d0-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="808d0-250">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="808d0-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="808d0-251">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="808d0-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="808d0-252">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="808d0-252">Testing single sign-on</span></span>

<span data-ttu-id="808d0-253">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="808d0-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="808d0-254">Щелкнув плитку DocuSign на панели доступа, вы автоматически войдете в приложение DocuSign.</span><span class="sxs-lookup"><span data-stu-id="808d0-254">When you click the DocuSign tile in the Access Panel, you should get automatically signed-on to your DocuSign application.</span></span>
<span data-ttu-id="808d0-255">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="808d0-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="808d0-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="808d0-256">Additional resources</span></span>

* [<span data-ttu-id="808d0-257">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="808d0-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="808d0-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="808d0-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="808d0-259">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="808d0-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

