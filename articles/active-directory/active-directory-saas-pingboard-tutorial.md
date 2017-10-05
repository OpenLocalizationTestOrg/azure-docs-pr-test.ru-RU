---
title: "Руководство по интеграции Azure Active Directory с Pingboard | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="9b7fe-103">Руководство по интеграции Azure Active Directory с Pingboard</span><span class="sxs-lookup"><span data-stu-id="9b7fe-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="9b7fe-104">В этом руководстве описано, как интегрировать приложение Pingboard с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b7fe-105">Интеграция Azure AD с Pingboard обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b7fe-106">С помощью Azure AD вы можете контролировать доступ к Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="9b7fe-107">Вы можете включить автоматический вход пользователей в Pingboard (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b7fe-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9b7fe-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b7fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9b7fe-110">Prerequisites</span></span>

<span data-ttu-id="9b7fe-111">Чтобы настроить интеграцию Azure AD с Pingboard, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="9b7fe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9b7fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b7fe-113">подписка Pingboard с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b7fe-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b7fe-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b7fe-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9b7fe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b7fe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9b7fe-118">Scenario description</span></span>
<span data-ttu-id="9b7fe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b7fe-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b7fe-121">Добавление Pingboard из коллекции</span><span class="sxs-lookup"><span data-stu-id="9b7fe-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="9b7fe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="9b7fe-123">Добавление Pingboard из коллекции</span><span class="sxs-lookup"><span data-stu-id="9b7fe-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="9b7fe-124">Чтобы настроить интеграцию Pingboard с Azure AD, необходимо добавить Pingboard из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b7fe-125">**Чтобы добавить Pingboard из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9b7fe-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b7fe-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b7fe-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b7fe-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9b7fe-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9b7fe-133">В поле поиска введите **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-133">In the search box, type **Pingboard**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="9b7fe-135">На панели результатов выберите **Pingboard** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b7fe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b7fe-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Pingboard с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b7fe-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Pingboard соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="9b7fe-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="9b7fe-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="9b7fe-142">Чтобы настроить и проверить единый вход Azure AD в Pingboard, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b7fe-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9b7fe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b7fe-145">**[Создание тестового пользователя Pingboard](#creating-a-pingboard-test-user)** требуется для создания в Pingboard пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9b7fe-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b7fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b7fe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b7fe-149">В этом разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="9b7fe-150">**Чтобы настроить единый вход Azure AD в Pingboard, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9b7fe-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="9b7fe-151">На портале управления Azure на странице интеграции с приложением **Pingboard** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9b7fe-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="9b7fe-155">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Pingboard** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9b7fe-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="9b7fe-157">а.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-157">a.</span></span> <span data-ttu-id="9b7fe-158">В текстовом поле **Идентификатор** введите значение `http://<entity-id>.pingboard.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="9b7fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-159">b.</span></span> <span data-ttu-id="9b7fe-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<entity-id>.pingboard.com/auth/saml/consume`.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b7fe-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-161">Please note that these are not the real values.</span></span> <span data-ttu-id="9b7fe-162">Необходимо указать фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9b7fe-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9b7fe-164">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Pingboard](https://support.pingboard.com/).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="9b7fe-165">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="9b7fe-167">а.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-167">a.</span></span> <span data-ttu-id="9b7fe-168">В текстовом поле **URL-адрес для входа** введите значение `http://<sub-domain>.pingboard.com/sign_in`.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="9b7fe-169">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="9b7fe-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9b7fe-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9b7fe-173">Чтобы настроить единый вход на стороне Pingboard, откройте новое окно браузера и войдите в учетную запись Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="9b7fe-174">Для настройки единого входа нужны права администратора Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="9b7fe-175">В верхнем меню выберите **Apps > Integrations** ("Приложения" > "Интеграция").</span><span class="sxs-lookup"><span data-stu-id="9b7fe-175">From the top menu select **Apps > Integrations**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="9b7fe-177">На странице **Integrations** (Интеграция) найдите элемент **Azure Active Directory** и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="9b7fe-179">В появившемся модальном окне щелкните **Configure** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-179">In the modal that follows click **"Configure"**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="9b7fe-181">На следующей странице вы увидите сообщение "Azure SSO Integration is enabled" (Интеграция для единого входа Azure включена).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="9b7fe-182">Откройте скачанный XML-файл метаданных в Блокноте и вставьте его содержимое в поле **IDP Metadata** (Метаданные IdP).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="9b7fe-184">Файл будет проверен, и если он пройдет проверку, то единый вход будет включен.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b7fe-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7fe-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b7fe-186">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9b7fe-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9b7fe-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b7fe-189">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b7fe-191">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b7fe-193">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b7fe-195">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b7fe-197">а.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-197">a.</span></span> <span data-ttu-id="9b7fe-198">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b7fe-199">b.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-199">b.</span></span> <span data-ttu-id="9b7fe-200">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b7fe-201">c.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-201">c.</span></span> <span data-ttu-id="9b7fe-202">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b7fe-203">d.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-203">d.</span></span> <span data-ttu-id="9b7fe-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="9b7fe-205">Создание тестового пользователя Pingboard</span><span class="sxs-lookup"><span data-stu-id="9b7fe-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="9b7fe-206">Чтобы пользователи Azure AD могли входить в Pingboard, их необходимо подготовить в Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="9b7fe-207">В случае с Pingboard подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="9b7fe-208">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9b7fe-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="9b7fe-209">Войдите на корпоративный сайт Pingboard в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="9b7fe-210">Нажмите кнопку **Add Employee** (Добавить сотрудника) на странице **Directory** (Каталог).</span><span class="sxs-lookup"><span data-stu-id="9b7fe-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="9b7fe-212">На диалоговой странице **Add Employee** (Добавление сотрудника) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="9b7fe-214">А.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-214">a.</span></span> <span data-ttu-id="9b7fe-215">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="9b7fe-216">b.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-216">b.</span></span> <span data-ttu-id="9b7fe-217">В текстовом поле **Электронная почта** введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="9b7fe-218">c.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-218">c.</span></span> <span data-ttu-id="9b7fe-219">В текстовом поле **Job Title** (Должность) введите должность пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="9b7fe-220">d.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-220">d.</span></span> <span data-ttu-id="9b7fe-221">Из раскрывающегося списка **Location** (Расположение) выберите расположение пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="9b7fe-222">д.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-222">e.</span></span> <span data-ttu-id="9b7fe-223">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-223">Click **Add**.</span></span>   

4. <span data-ttu-id="9b7fe-224">Откроется окно подтверждения добавления пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![Подтверждение](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="9b7fe-226">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b7fe-227">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7fe-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b7fe-228">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к PingBoard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9b7fe-230">**Чтобы назначить пользователя Britta Simon в Pingboard, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9b7fe-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="9b7fe-231">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9b7fe-233">В списке приложений выберите **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-233">In the applications list, select **Pingboard**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="9b7fe-235">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9b7fe-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-237">Click **Add** button.</span></span> <span data-ttu-id="9b7fe-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9b7fe-240">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9b7fe-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b7fe-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b7fe-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9b7fe-243">Testing single sign-on</span></span>

<span data-ttu-id="9b7fe-244">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b7fe-245">Щелкнув элемент Pingboard на панели доступа, вы автоматически войдете в приложение Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b7fe-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b7fe-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9b7fe-246">Additional resources</span></span>

* [<span data-ttu-id="9b7fe-247">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b7fe-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b7fe-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b7fe-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
