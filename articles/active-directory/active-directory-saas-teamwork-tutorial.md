---
title: "Руководство по интеграции Azure Active Directory с Teamwork | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Teamwork."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="e7785-103">Руководство по интеграции Azure Active Directory с Teamwork</span><span class="sxs-lookup"><span data-stu-id="e7785-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="e7785-104">В этом руководстве описано, как интегрировать Teamwork с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7785-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7785-105">Интеграция Azure AD с приложением Teamwork обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e7785-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7785-106">С помощью Azure AD вы можете контролировать доступ к Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="e7785-107">Вы можете включить автоматический вход пользователей в Teamwork (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7785-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7785-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="e7785-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e7785-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7785-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7785-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e7785-110">Prerequisites</span></span>

<span data-ttu-id="e7785-111">Чтобы настроить интеграцию Azure AD с Teamwork, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="e7785-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="e7785-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e7785-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7785-113">подписка на Teamwork с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e7785-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="e7785-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e7785-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e7785-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e7785-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7785-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="e7785-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e7785-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7785-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e7785-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e7785-118">Scenario description</span></span>
<span data-ttu-id="e7785-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e7785-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7785-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e7785-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7785-121">Добавление Teamwork из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e7785-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="e7785-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7785-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="e7785-123">Добавление Teamwork из коллекции</span><span class="sxs-lookup"><span data-stu-id="e7785-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="e7785-124">Чтобы настроить интеграцию Teamwork в Azure AD, вам необходимо добавить Teamwork из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7785-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7785-125">**Чтобы добавить Teamwork из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e7785-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7785-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7785-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7785-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e7785-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7785-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e7785-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e7785-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e7785-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e7785-133">Введите в поле поиска **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="e7785-133">In the search box, type **Teamwork**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="e7785-135">На панели результатов выберите **Teamwork** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e7785-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7785-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7785-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7785-138">В этом разделе описана настройка и проверка единого входа Azure AD в Teamwork с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7785-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7785-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Teamwork соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7785-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="e7785-140">Другими словами — необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="e7785-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD, которое будет соответствовать **имени пользователя** в Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="e7785-142">Чтобы настроить и проверить единый вход Azure AD в Teamwork, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="e7785-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7785-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e7785-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7785-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7785-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7785-145">**[Создание тестового пользователя Teamwork](#creating-a-teamwork-test-user)** требуется для создания в Teamwork пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7785-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e7785-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7785-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7785-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e7785-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7785-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7785-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7785-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure, а также как его настроить в приложении Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="e7785-150">**Чтобы настроить единый вход Azure AD в Teamwork, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e7785-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="e7785-151">На портале управления Azure на странице интеграции с приложением **Teamwork** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e7785-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e7785-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e7785-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="e7785-155">В текстовом поле **URL-адрес для входа** раздела **Домены и URL-адреса приложения Teamwork** введите URL-адрес в следующем формате: `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="e7785-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="e7785-157">Обратите внимание, что это значение используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e7785-157">Please note that this is not the real value.</span></span> <span data-ttu-id="e7785-158">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="e7785-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="e7785-159">Чтобы получить это значение, обратитесь в [службу поддержки Teamwork](mailto:support@teamwork.com).</span><span class="sxs-lookup"><span data-stu-id="e7785-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="e7785-160">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="e7785-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="e7785-162">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите **дату окончания срока действия**.</span><span class="sxs-lookup"><span data-stu-id="e7785-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="e7785-163">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e7785-163">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="e7785-165">В разделе **Сертификат подписи SAML** выберите **Make new certificate active** (Сделать новый сертификат активным) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e7785-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="e7785-167">Во всплывающем окне **Rollover certificate** (Сертификат восстановления) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e7785-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e7785-169">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e7785-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="e7785-171">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки Teamwork](mailto:support@teamwork.com) и предоставьте скачанный **файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="e7785-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7785-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7785-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7785-173">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7785-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e7785-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e7785-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7785-176">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e7785-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7785-178">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="e7785-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7785-180">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e7785-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7785-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e7785-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7785-184">а.</span><span class="sxs-lookup"><span data-stu-id="e7785-184">a.</span></span> <span data-ttu-id="e7785-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7785-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7785-186">b.</span><span class="sxs-lookup"><span data-stu-id="e7785-186">b.</span></span> <span data-ttu-id="e7785-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7785-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7785-188">c.</span><span class="sxs-lookup"><span data-stu-id="e7785-188">c.</span></span> <span data-ttu-id="e7785-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e7785-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7785-190">d.</span><span class="sxs-lookup"><span data-stu-id="e7785-190">d.</span></span> <span data-ttu-id="e7785-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e7785-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="e7785-192">Создание тестового пользователя Teamwork</span><span class="sxs-lookup"><span data-stu-id="e7785-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="e7785-193">В этом разделе описано, как создать пользователя Britta Simon в Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="e7785-194">Обратитесь в [службу поддержки Teamwork](mailto:support@teamwork.com), чтобы добавить пользователей на платформу Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7785-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7785-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7785-196">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e7785-198">**Чтобы назначить пользователя Britta Simon в Teamwork, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e7785-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="e7785-199">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e7785-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e7785-201">В списке приложений выберите **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="e7785-201">In the applications list, select **Teamwork**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="e7785-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e7785-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e7785-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e7785-205">Click **Add** button.</span></span> <span data-ttu-id="e7785-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e7785-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e7785-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e7785-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7785-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e7785-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7785-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e7785-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="e7785-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e7785-211">Testing single sign-on</span></span>

<span data-ttu-id="e7785-212">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e7785-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7785-213">Щелкнув плитку Teamwork на панели доступа, вы автоматически войдете в приложение Teamwork.</span><span class="sxs-lookup"><span data-stu-id="e7785-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e7785-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e7785-214">Additional resources</span></span>

* [<span data-ttu-id="e7785-215">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7785-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7785-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7785-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png