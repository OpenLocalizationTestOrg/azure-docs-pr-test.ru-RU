---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="0c29c-103">Учебник. Интеграция Azure Active Directory с песочницей Salesforce</span><span class="sxs-lookup"><span data-stu-id="0c29c-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="0c29c-104">В этом руководстве описано, как интегрировать Salesforce Sandbox с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c29c-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c29c-105">Интеграция Azure AD с Salesforce Sandbox обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0c29c-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c29c-106">С помощью Azure AD можно управлять доступом к Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="0c29c-107">Вы можете включить автоматический вход пользователей в Salesforce Sandbox (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c29c-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c29c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0c29c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0c29c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c29c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c29c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0c29c-110">Prerequisites</span></span>

<span data-ttu-id="0c29c-111">Чтобы настроить интеграцию Azure AD с Salesforce Sandbox, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0c29c-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="0c29c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0c29c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c29c-113">подписка Salesforce Sandbox с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0c29c-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c29c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0c29c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c29c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0c29c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c29c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0c29c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c29c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c29c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c29c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0c29c-118">Scenario description</span></span>
<span data-ttu-id="0c29c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0c29c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c29c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0c29c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c29c-121">Добавление Salesforce Sandbox из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0c29c-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="0c29c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c29c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="0c29c-123">Добавление Salesforce Sandbox из коллекции</span><span class="sxs-lookup"><span data-stu-id="0c29c-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="0c29c-124">Чтобы настроить интеграцию Salesforce Sandbox с Azure AD, нужно добавить Salesforce Sandbox из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0c29c-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c29c-125">**Чтобы добавить Salesforce Sandbox из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0c29c-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c29c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0c29c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c29c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0c29c-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0c29c-133">В поле поиска введите **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="0c29c-135">На панели результатов выберите **Salesforce Sandbox** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="0c29c-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c29c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c29c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c29c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Salesforce Sandbox с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c29c-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0c29c-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Salesforce Sandbox соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c29c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="0c29c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="0c29c-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="0c29c-142">Чтобы настроить и проверить единый вход Azure AD в Salesforce Sandbox, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="0c29c-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c29c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0c29c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0c29c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c29c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c29c-145">**[Создание тестового пользователя Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)** требуется для того, чтобы в Salesforce Sandbox существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c29c-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c29c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c29c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c29c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0c29c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c29c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c29c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c29c-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="0c29c-150">**Чтобы настроить единый вход Azure AD в Salesforce Sandbox, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0c29c-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="0c29c-151">На портале Azure на странице интеграции с приложением **Salesforce Sandbox** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0c29c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0c29c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="0c29c-155">В разделе **Домен и URL-адреса Salesforce Sandbox** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c29c-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="0c29c-157">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<subdomain>.my.salesforce.com`.</span><span class="sxs-lookup"><span data-stu-id="0c29c-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0c29c-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="0c29c-158">This value is not the real.</span></span> <span data-ttu-id="0c29c-159">Замените это значение фактическим URL-адресом входа. Обратитесь к [группе поддержки клиентов Salesforce Sandbox](https://help.salesforce.com/support) для получения этого значения.</span><span class="sxs-lookup"><span data-stu-id="0c29c-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="0c29c-160">Если вы уже настроили единый вход для другого экземпляра Salesforce Sandbox в каталоге, необходимо также настроить параметр **Идентификатор**, задав для него то же значение, что и для параметра **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="0c29c-161">Поле **Идентификатор** можно найти, установив флажок **Показать дополнительные настройки** на странице **Настроить URL-адрес приложения** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0c29c-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="0c29c-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0c29c-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="0c29c-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0c29c-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0c29c-166">В разделе **Конфигурация Salesforce Sandbox** щелкните **Настроить Salesforce Sandbox**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c29c-167">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="0c29c-168">![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="0c29c-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="0c29c-169">Откройте новую вкладку в браузере и войдите в учетную запись администратора Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="0c29c-170">В верхнем меню щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-170">In the menu on the top, click **Setup**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="0c29c-172">В области навигации слева щелкните **Security Controls** (Средства управления безопасностью), а затем — **Параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="0c29c-174">В разделе "Single Sign-On Settings" (Параметры единого входа) сделайте следующее. ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="0c29c-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="0c29c-175">а.</span><span class="sxs-lookup"><span data-stu-id="0c29c-175">a.</span></span>  <span data-ttu-id="0c29c-176">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="0c29c-177">b.</span><span class="sxs-lookup"><span data-stu-id="0c29c-177">b.</span></span>  <span data-ttu-id="0c29c-178">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-178">Click **New**.</span></span>

12. <span data-ttu-id="0c29c-179">В разделе «Параметры единого входа SAML» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0c29c-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="0c29c-181">В текстовое поле "Name" (Имя) введите имя конфигурации (например, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="0c29c-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="0c29c-182">b.</span><span class="sxs-lookup"><span data-stu-id="0c29c-182">b.</span></span> <span data-ttu-id="0c29c-183">Вставьте значение **SAML Entity ID** (Идентификатор сущности SAML) в поле **Issuer** (Издатель).</span><span class="sxs-lookup"><span data-stu-id="0c29c-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="0c29c-184">c.</span><span class="sxs-lookup"><span data-stu-id="0c29c-184">c.</span></span> <span data-ttu-id="0c29c-185">В текстовом поле **Entity Id** (Идентификатор сущности) введите **https://test.salesforce.com**, если это первый экземпляр Salesforce Sandbox, добавляемый в каталог.</span><span class="sxs-lookup"><span data-stu-id="0c29c-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="0c29c-186">Если вы уже добавили экземпляр Salesforce Sandbox, то для параметра **Идентификатор сущности** введите значение **URL-адрес входа** в следующем формате: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0c29c-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="0c29c-187">d.</span><span class="sxs-lookup"><span data-stu-id="0c29c-187">d.</span></span> <span data-ttu-id="0c29c-188">Чтобы отправить скачанный сертификат, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="0c29c-189">д.</span><span class="sxs-lookup"><span data-stu-id="0c29c-189">e.</span></span> <span data-ttu-id="0c29c-190">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains the Federation ID from the User object** (Проверочное утверждение содержит идентификатор федерации из объекта User).</span><span class="sxs-lookup"><span data-stu-id="0c29c-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="0c29c-191">Е.</span><span class="sxs-lookup"><span data-stu-id="0c29c-191">f.</span></span> <span data-ttu-id="0c29c-192">В поле **SAML Identity Location** (Расположение удостоверения SAML) выберите значение **Identity is in the NameIdentifier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="0c29c-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="0c29c-193">g.</span><span class="sxs-lookup"><span data-stu-id="0c29c-193">g.</span></span> <span data-ttu-id="0c29c-194">Вставьте **URL-адрес службы единого входа** в текстовое поле **Identity Provider Login URL** (URL-адрес входа поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="0c29c-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="0c29c-195">h.</span><span class="sxs-lookup"><span data-stu-id="0c29c-195">h.</span></span> <span data-ttu-id="0c29c-196">SFDC не поддерживает выход SAML.</span><span class="sxs-lookup"><span data-stu-id="0c29c-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="0c29c-197">Чтобы обойти эту проблему, вставьте значение https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0 в текстовое поле **URL-адрес для выхода поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="0c29c-198">i.</span><span class="sxs-lookup"><span data-stu-id="0c29c-198">i.</span></span> <span data-ttu-id="0c29c-199">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="0c29c-200">j.</span><span class="sxs-lookup"><span data-stu-id="0c29c-200">j.</span></span> <span data-ttu-id="0c29c-201">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="0c29c-202">Включение домена</span><span class="sxs-lookup"><span data-stu-id="0c29c-202">Enable your domain</span></span>
<span data-ttu-id="0c29c-203">В этом разделе предполагается, что вы уже создали домен.</span><span class="sxs-lookup"><span data-stu-id="0c29c-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="0c29c-204">Дополнительные сведения см. в разделе [Define Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Определение доменного имени).</span><span class="sxs-lookup"><span data-stu-id="0c29c-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="0c29c-205">**Выполните следующие действия, чтобы включить домен:**</span><span class="sxs-lookup"><span data-stu-id="0c29c-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="0c29c-206">В области навигации слева щелкните **Управление доменами**, затем — **Мой домен**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="0c29c-208">Убедитесь в правильности настройки домена.</span><span class="sxs-lookup"><span data-stu-id="0c29c-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="0c29c-209">В разделе **Login Page Settings** (Параметры страницы входа) щелкните **Изменить**, а затем для параметра **Authentication Service** (Служба проверки подлинности) выберите имя параметра единого входа SAML из предыдущего раздела, после чего щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="0c29c-211">После настройки домена для входа в песочницу Salesforce пользователям необходимо будет использовать URL-адрес домена.</span><span class="sxs-lookup"><span data-stu-id="0c29c-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="0c29c-212">Чтобы получить значение URL-адреса, щелкните профиль единого входа, созданный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="0c29c-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="0c29c-213">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0c29c-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0c29c-214">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0c29c-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0c29c-215">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0c29c-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c29c-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c29c-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c29c-217">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c29c-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0c29c-219">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0c29c-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c29c-220">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c29c-222">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c29c-224">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c29c-226">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c29c-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c29c-228">а.</span><span class="sxs-lookup"><span data-stu-id="0c29c-228">a.</span></span> <span data-ttu-id="0c29c-229">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c29c-230">b.</span><span class="sxs-lookup"><span data-stu-id="0c29c-230">b.</span></span> <span data-ttu-id="0c29c-231">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c29c-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c29c-232">c.</span><span class="sxs-lookup"><span data-stu-id="0c29c-232">c.</span></span> <span data-ttu-id="0c29c-233">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0c29c-234">d.</span><span class="sxs-lookup"><span data-stu-id="0c29c-234">d.</span></span> <span data-ttu-id="0c29c-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="0c29c-236">Создание тестового пользователя Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0c29c-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="0c29c-237">В этом разделе вы создадите в Salesforce Sandbox пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c29c-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="0c29c-238">Salesforce Sandbox поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0c29c-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="0c29c-239">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="0c29c-239">There is no action item for you in this section.</span></span> <span data-ttu-id="0c29c-240">Если пользователь в Salesforce Sandbox еще не существует, он создается при попытке доступа к Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0c29c-241">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c29c-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0c29c-242">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0c29c-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0c29c-244">**Чтобы назначить пользователя Britta Simon в Salesforce Sandbox, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0c29c-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="0c29c-245">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0c29c-247">Из списка приложений выберите **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="0c29c-249">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0c29c-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-251">Click **Add** button.</span></span> <span data-ttu-id="0c29c-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0c29c-254">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0c29c-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c29c-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0c29c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c29c-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0c29c-257">Testing single sign-on</span></span>

<span data-ttu-id="0c29c-258">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="0c29c-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="0c29c-259">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c29c-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c29c-260">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0c29c-260">Additional resources</span></span>

* [<span data-ttu-id="0c29c-261">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c29c-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c29c-262">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c29c-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0c29c-263">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="0c29c-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

