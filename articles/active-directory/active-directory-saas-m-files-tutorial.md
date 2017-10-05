---
title: "Учебник. Интеграция Azure Active Directory с M-Files | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в M-Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="78dd4-103">Учебник. Интеграция Azure Active Directory с M-Files</span><span class="sxs-lookup"><span data-stu-id="78dd4-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="78dd4-104">В этом учебнике описано, как интегрировать приложение M-Files с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78dd4-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78dd4-105">Интеграция Azure AD с приложением M-Files обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="78dd4-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78dd4-106">С помощью Azure AD вы можете контролировать доступ к M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="78dd4-107">Вы можете включить автоматический вход пользователей в M-Files (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78dd4-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="78dd4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78dd4-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78dd4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78dd4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78dd4-110">Prerequisites</span></span>

<span data-ttu-id="78dd4-111">Чтобы настроить интеграцию Azure AD с M-Files, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="78dd4-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="78dd4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="78dd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78dd4-113">подписка M-Files с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="78dd4-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78dd4-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="78dd4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78dd4-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="78dd4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78dd4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="78dd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78dd4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78dd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78dd4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="78dd4-118">Scenario description</span></span>
<span data-ttu-id="78dd4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="78dd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78dd4-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="78dd4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78dd4-121">Добавление M-Files из коллекции</span><span class="sxs-lookup"><span data-stu-id="78dd4-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="78dd4-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="78dd4-123">Добавление M-Files из коллекции</span><span class="sxs-lookup"><span data-stu-id="78dd4-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="78dd4-124">Чтобы настроить интеграцию M-Files с Azure AD, необходимо добавить M-Files из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="78dd4-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78dd4-125">**Чтобы добавить M-Files из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="78dd4-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78dd4-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78dd4-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78dd4-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="78dd4-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="78dd4-133">В поле поиска введите **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-133">In the search box, type **M-Files**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="78dd4-135">На панели результатов выберите **M-Files** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="78dd4-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78dd4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78dd4-138">В этом разделе описана настройка и проверка единого входа Azure AD в M-Files с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78dd4-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="78dd4-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="78dd4-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78dd4-142">Чтобы настроить и проверить единый вход Azure AD в M-Files, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="78dd4-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78dd4-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="78dd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78dd4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78dd4-145">**[Создание тестового пользователя M-Files](#creating-a-m-files-test-user)** требуется для создания в M-Files пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78dd4-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78dd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="78dd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78dd4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78dd4-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="78dd4-150">**Чтобы настроить единый вход Azure AD в M-Files, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="78dd4-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="78dd4-151">На портале Azure на странице интеграции с приложением **M-Files** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="78dd4-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="78dd4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="78dd4-155">В разделе **Домены и URL-адреса приложения M-Files** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="78dd4-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="78dd4-157">а.</span><span class="sxs-lookup"><span data-stu-id="78dd4-157">a.</span></span> <span data-ttu-id="78dd4-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="78dd4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="78dd4-159">b.</span><span class="sxs-lookup"><span data-stu-id="78dd4-159">b.</span></span> <span data-ttu-id="78dd4-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="78dd4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78dd4-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="78dd4-161">These values are not real.</span></span> <span data-ttu-id="78dd4-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="78dd4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78dd4-163">Чтобы получить их, обратитесь в [службу поддержки клиентов M-Files](mailto:support@m-files.com).</span><span class="sxs-lookup"><span data-stu-id="78dd4-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="78dd4-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="78dd4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="78dd4-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="78dd4-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78dd4-168">Для настройки единого входа в вашем приложении обратитесь в [службу поддержки M-Files](mailto:support@m-files.com) и предоставьте скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="78dd4-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="78dd4-169">Если вы хотите настроить единый вход для классического приложения M-Files, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="78dd4-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="78dd4-170">Если единый вход настраивается только для веб-версии M-Files, то никакие дополнительные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="78dd4-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="78dd4-171">Выполните описанные ниже действия, чтобы настроить в классическом приложении M-Files единый вход с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="78dd4-172">Для скачивания M-Files перейдите на страницу [M-Files download](https://www.m-files.com/en/download-latest-version) (Скачивание M-Files).</span><span class="sxs-lookup"><span data-stu-id="78dd4-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="78dd4-173">Откройте окно **M-Files Desktop Settings** (Параметры классического приложения M-Files).</span><span class="sxs-lookup"><span data-stu-id="78dd4-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="78dd4-174">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-174">Then, click **Add**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="78dd4-176">В окне **Document Vault Connection Properties** (Свойства подключения хранилища документов) выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="78dd4-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="78dd4-178">В разделе Server (Сервер) введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="78dd4-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="78dd4-179">а.</span><span class="sxs-lookup"><span data-stu-id="78dd4-179">a.</span></span> <span data-ttu-id="78dd4-180">В поле **Name** (Имя) введите `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="78dd4-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="78dd4-181">b.</span><span class="sxs-lookup"><span data-stu-id="78dd4-181">b.</span></span> <span data-ttu-id="78dd4-182">В поле **Port Number** (Номер порта) введите **4466**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="78dd4-183">c.</span><span class="sxs-lookup"><span data-stu-id="78dd4-183">c.</span></span> <span data-ttu-id="78dd4-184">Для параметра **Protocol** (Протокол) выберите **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="78dd4-185">d.</span><span class="sxs-lookup"><span data-stu-id="78dd4-185">d.</span></span> <span data-ttu-id="78dd4-186">В поле **Authentication** (Аутентификация) выберите **Specific Windows user** (Определенный пользователь Windows).</span><span class="sxs-lookup"><span data-stu-id="78dd4-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="78dd4-187">Затем отобразится страница подписи.</span><span class="sxs-lookup"><span data-stu-id="78dd4-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="78dd4-188">Введите свои учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78dd4-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="78dd4-189">д.</span><span class="sxs-lookup"><span data-stu-id="78dd4-189">e.</span></span> <span data-ttu-id="78dd4-190">Для параметра **Vault on Server** (Хранилище на сервере) выберите соответствующее хранилище на сервере.</span><span class="sxs-lookup"><span data-stu-id="78dd4-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="78dd4-191">Е.</span><span class="sxs-lookup"><span data-stu-id="78dd4-191">f.</span></span> <span data-ttu-id="78dd4-192">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="78dd4-193">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="78dd4-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78dd4-194">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="78dd4-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78dd4-195">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="78dd4-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78dd4-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="78dd4-197">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="78dd4-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="78dd4-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78dd4-200">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78dd4-202">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78dd4-204">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78dd4-206">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="78dd4-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78dd4-208">а.</span><span class="sxs-lookup"><span data-stu-id="78dd4-208">a.</span></span> <span data-ttu-id="78dd4-209">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78dd4-210">b.</span><span class="sxs-lookup"><span data-stu-id="78dd4-210">b.</span></span> <span data-ttu-id="78dd4-211">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78dd4-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78dd4-212">c.</span><span class="sxs-lookup"><span data-stu-id="78dd4-212">c.</span></span> <span data-ttu-id="78dd4-213">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78dd4-214">d.</span><span class="sxs-lookup"><span data-stu-id="78dd4-214">d.</span></span> <span data-ttu-id="78dd4-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="78dd4-216">Создание тестового пользователя M-Files</span><span class="sxs-lookup"><span data-stu-id="78dd4-216">Creating a M-Files test user</span></span>

<span data-ttu-id="78dd4-217">Цель этого раздела — создать пользователя с именем Britta Simon в приложении M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="78dd4-218">Обратитесь в [службу поддержки M-Files](mailto:support@m-files.com), чтобы добавить пользователей в приложение M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78dd4-219">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="78dd4-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78dd4-220">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="78dd4-222">**Чтобы назначить пользователя Britta Simon в M-Files, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="78dd4-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="78dd4-223">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="78dd4-225">В списке приложений выберите **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-225">In the applications list, select **M-Files**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="78dd4-227">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="78dd4-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-229">Click **Add** button.</span></span> <span data-ttu-id="78dd4-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="78dd4-232">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78dd4-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78dd4-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="78dd4-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78dd4-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="78dd4-235">Testing single sign-on</span></span>

<span data-ttu-id="78dd4-236">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="78dd4-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="78dd4-237">Щелкнув элемент M-Files на панели доступа, вы автоматически войдете в приложение M-Files.</span><span class="sxs-lookup"><span data-stu-id="78dd4-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78dd4-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="78dd4-238">Additional resources</span></span>

* [<span data-ttu-id="78dd4-239">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78dd4-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78dd4-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78dd4-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

