---
title: "Руководство по интеграции Azure Active Directory с 8x8 Virtual Office | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и 8x8 Virtual Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="9d7ec-103">Руководство. Интеграция Azure Active Directory с 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="9d7ec-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="9d7ec-104">В этом руководстве описано, как интегрировать 8x8 Virtual Office с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d7ec-105">Интеграция 8x8 Virtual Office с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d7ec-106">С помощью Azure AD вы можете контролировать доступ к 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="9d7ec-107">Вы можете включить автоматический вход пользователей в 8x8 Virtual Office (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d7ec-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d7ec-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d7ec-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9d7ec-110">Prerequisites</span></span>

<span data-ttu-id="9d7ec-111">Чтобы настроить интеграцию Azure AD с 8x8 Virtual Office, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="9d7ec-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9d7ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d7ec-113">подписка 8x8 Virtual Office с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d7ec-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d7ec-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d7ec-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d7ec-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d7ec-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9d7ec-118">Scenario description</span></span>
<span data-ttu-id="9d7ec-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d7ec-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d7ec-121">Добавление 8x8 Virtual Office из коллекции.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="9d7ec-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d7ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="9d7ec-123">Добавление 8x8 Virtual Office из коллекции.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="9d7ec-124">Чтобы настроить интеграцию приложения 8x8 Virtual Office с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d7ec-125">**Чтобы добавить 8x8 Virtual Office из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="9d7ec-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d7ec-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d7ec-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d7ec-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9d7ec-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9d7ec-133">В поле поиска введите **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="9d7ec-135">В области результатов выберите **8x8 Virtual Office** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d7ec-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d7ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d7ec-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение 8x8 Virtual Office с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d7ec-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в 8x8 Virtual Office соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="9d7ec-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="9d7ec-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d7ec-142">Чтобы настроить и проверить единый вход Azure AD в 8x8 Virtual Office, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d7ec-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d7ec-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d7ec-145">**[Создание тестового пользователя 8x8 Virtual Office](#creating-a-8x8-virtual-office-test-user)** нужно для того, чтобы в 8x8 Virtual Office также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d7ec-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d7ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d7ec-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d7ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d7ec-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="9d7ec-150">**Чтобы настроить единый вход Azure AD в 8x8 Virtual Office, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="9d7ec-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="9d7ec-151">На портале Azure на странице интеграции с приложением **8x8 Virtual Office** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9d7ec-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="9d7ec-155">В разделе **Домены и URL-адреса приложения 8x8 Virtual Office** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="9d7ec-157">а.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-157">a.</span></span> <span data-ttu-id="9d7ec-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="9d7ec-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="9d7ec-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="9d7ec-160">b.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-160">b.</span></span> <span data-ttu-id="9d7ec-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="9d7ec-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="9d7ec-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="9d7ec-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d7ec-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-163">These values are not real.</span></span> <span data-ttu-id="9d7ec-164">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9d7ec-165">Обратитесь к [группе поддержки 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="9d7ec-166">В разделе **Сертификат подписи SAML** щелкните **Certificate (Raw)** (Сертификат (необработанный)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="9d7ec-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9d7ec-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d7ec-170">В разделе **Конфигурация 8x8 Virtual Office** щелкните **Настроить 8x8 Virtual Office**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d7ec-171">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="9d7ec-173">Войдите в клиент 8x8 Virtual Office от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="9d7ec-174">На панели приложения выберите **Virtual Office Account Mgr** (Диспетчер учетных записей Virtual Office).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="9d7ec-176">Выберите в качестве учетной записи, которой нужно управлять, **Business** (Рабочая) и нажмите кнопку **Sign In** (Вход).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="9d7ec-178">В списке меню щелкните вкладку **Accounts** (Учетные записи).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="9d7ec-180">В списке Accounts (Учетные записи) щелкните **Single Sign On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="9d7ec-182">В разделе "Authentication method" (Метод проверки подлинности) установите флажок **Signle Sign On** (Единый вход), а затем установите переключатель **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="9d7ec-184">Скопируйте значения параметров **URL-адрес единого входа SAML**, **Single Sing Out Service URL** (URL-адрес службы единого выхода) и **URL-адрес издателя** из Azure AD и вставьте их в качестве значений параметров **Sign In URL** (URL-адрес входа), **Sign Out URL** (URL-адрес выхода) и **Issuer URL** (URL-адрес издателя) в приложении 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Настройка на стороне приложения](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="9d7ec-186">Нажмите кнопку **Browser** (Обзор), чтобы отправить сертификат, скачанный из Azure AD, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="9d7ec-187">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d7ec-188">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d7ec-189">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d7ec-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d7ec-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d7ec-191">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9d7ec-193">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9d7ec-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d7ec-194">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d7ec-196">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d7ec-198">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d7ec-200">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d7ec-202">а.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-202">a.</span></span> <span data-ttu-id="9d7ec-203">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d7ec-204">b.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-204">b.</span></span> <span data-ttu-id="9d7ec-205">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d7ec-206">c.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-206">c.</span></span> <span data-ttu-id="9d7ec-207">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d7ec-208">d.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-208">d.</span></span> <span data-ttu-id="9d7ec-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="9d7ec-210">Создание тестового пользователя 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="9d7ec-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="9d7ec-211">Цель этого раздела — создать пользователя с именем Britta Simon в приложении 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="9d7ec-212">Приложение 8x8 Virtual Office поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9d7ec-213">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-213">There is no action item for you in this section.</span></span> <span data-ttu-id="9d7ec-214">Пользователь будет создан при попытке получить доступ к приложению 8x8 Virtual Office (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="9d7ec-215">Чтобы создать пользователя вручную, необходимо обратиться к [группе поддержки 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d7ec-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d7ec-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d7ec-217">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9d7ec-219">**Чтобы назначить пользователя Britta Simon в 8x8 Virtual Office, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9d7ec-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="9d7ec-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9d7ec-222">В списке приложений выберите **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="9d7ec-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9d7ec-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-226">Click **Add** button.</span></span> <span data-ttu-id="9d7ec-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9d7ec-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d7ec-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d7ec-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d7ec-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9d7ec-232">Testing single sign-on</span></span>

<span data-ttu-id="9d7ec-233">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d7ec-234">Щелкнув элемент 8x8 Virtual Office на панели доступа, вы автоматически войдете в приложение 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9d7ec-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="9d7ec-235">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d7ec-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d7ec-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d7ec-236">Additional resources</span></span>

* [<span data-ttu-id="9d7ec-237">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d7ec-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d7ec-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d7ec-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

