---
title: "Учебник. Интеграция Azure Active Directory с Skillport | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="91819-103">Руководство по интеграции Azure Active Directory с Skillport</span><span class="sxs-lookup"><span data-stu-id="91819-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="91819-104">В этом руководстве описано, как интегрировать Skillport с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91819-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91819-105">Интеграция Azure AD с приложением Skillport обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="91819-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91819-106">С помощью Azure AD вы можете контролировать доступ к Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="91819-107">Вы можете включить автоматический вход пользователей в Skillport (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91819-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91819-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="91819-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91819-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91819-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91819-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="91819-110">Prerequisites</span></span>

<span data-ttu-id="91819-111">Чтобы настроить интеграцию Azure AD с Skillport, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="91819-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="91819-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="91819-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91819-113">подписка на Skillport с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="91819-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91819-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="91819-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91819-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="91819-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91819-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="91819-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91819-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91819-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91819-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="91819-118">Scenario description</span></span>
<span data-ttu-id="91819-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="91819-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91819-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="91819-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91819-121">Добавление Skillport из коллекции</span><span class="sxs-lookup"><span data-stu-id="91819-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="91819-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="91819-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="91819-123">Добавление Skillport из коллекции</span><span class="sxs-lookup"><span data-stu-id="91819-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="91819-124">Чтобы настроить интеграцию приложения Skillport с Azure AD, вам нужно добавить Skillport из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="91819-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91819-125">**Чтобы добавить Skillport из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="91819-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91819-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91819-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91819-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="91819-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91819-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="91819-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="91819-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="91819-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="91819-133">В поле поиска введите **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="91819-133">In the search box, type **Skillport**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="91819-135">На панели результатов выберите **Skillport** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="91819-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91819-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="91819-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91819-138">В этом разделе описана настройка и проверка единого входа Azure AD в Skillport с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91819-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91819-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Skillport соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91819-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="91819-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="91819-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="91819-142">Чтобы настроить и проверить единый вход Azure AD в Skillport, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="91819-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91819-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="91819-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91819-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91819-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91819-145">**[Создание тестового пользователя Skillport](#creating-a-skillport-test-user)** требуется для создания в Skillport пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91819-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="91819-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91819-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91819-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="91819-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91819-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="91819-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91819-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="91819-150">**Чтобы настроить единый вход Azure AD в Skillport, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="91819-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="91819-151">На портале Azure на странице интеграции с приложением **Skillport** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="91819-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="91819-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="91819-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="91819-155">В разделе **Домены и URL-адреса приложения Skillport** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="91819-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="91819-157">а.</span><span class="sxs-lookup"><span data-stu-id="91819-157">a.</span></span> <span data-ttu-id="91819-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="91819-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="91819-159">Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="91819-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="91819-160">Центр обработки данных в США: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="91819-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="91819-161">b.</span><span class="sxs-lookup"><span data-stu-id="91819-161">b.</span></span> <span data-ttu-id="91819-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="91819-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="91819-163">Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="91819-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="91819-164">Центр обработки данных в США: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="91819-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91819-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="91819-165">These values are not the real.</span></span> <span data-ttu-id="91819-166">Измените их на фактические значения URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="91819-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="91819-167">Чтобы получить их, обратитесь в [службу поддержки клиентов Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="91819-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="91819-168">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="91819-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="91819-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="91819-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91819-172">Чтобы настроить единый вход на стороне **Skillport**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="91819-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="91819-173">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="91819-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91819-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="91819-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="91819-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91819-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="91819-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="91819-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91819-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91819-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91819-180">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="91819-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91819-182">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="91819-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91819-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="91819-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91819-186">а.</span><span class="sxs-lookup"><span data-stu-id="91819-186">a.</span></span> <span data-ttu-id="91819-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91819-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91819-188">b.</span><span class="sxs-lookup"><span data-stu-id="91819-188">b.</span></span> <span data-ttu-id="91819-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91819-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91819-190">c.</span><span class="sxs-lookup"><span data-stu-id="91819-190">c.</span></span> <span data-ttu-id="91819-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="91819-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91819-192">d.</span><span class="sxs-lookup"><span data-stu-id="91819-192">d.</span></span> <span data-ttu-id="91819-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="91819-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="91819-194">Создание тестового пользователя Skillport</span><span class="sxs-lookup"><span data-stu-id="91819-194">Creating a Skillport test user</span></span>

<span data-ttu-id="91819-195">Чтобы создать тестового пользователя Skillport, обратитесь в [службу поддержки Skillport](https://www.skillsoft.com/contact.asp), так как они поддерживают различные бизнес-сценарии в соответствии с требованиями пользователей.</span><span class="sxs-lookup"><span data-stu-id="91819-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="91819-196">Специалисты выполнят настройку после обсуждения с пользователями.</span><span class="sxs-lookup"><span data-stu-id="91819-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91819-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="91819-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91819-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="91819-200">**Чтобы назначить пользователя Britta Simon приложению Skillport, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="91819-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="91819-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="91819-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="91819-203">В списке приложений выберите **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="91819-203">In the applications list, select **Skillport**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="91819-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="91819-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="91819-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="91819-207">Click **Add** button.</span></span> <span data-ttu-id="91819-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="91819-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="91819-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="91819-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="91819-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="91819-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91819-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="91819-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91819-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="91819-213">Testing single sign-on</span></span>

<span data-ttu-id="91819-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="91819-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91819-215">Щелкнув элемент Skillport на панели доступа, вы автоматически войдете в приложение Skillport.</span><span class="sxs-lookup"><span data-stu-id="91819-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="91819-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="91819-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91819-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="91819-217">Additional resources</span></span>

* [<span data-ttu-id="91819-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91819-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91819-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91819-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

