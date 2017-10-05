---
title: "Учебник. Интеграция Azure Active Directory с Lynda.com | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="f1c8f-103">Руководство. Интеграция Azure Active Directory с Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f1c8f-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="f1c8f-104">В этом руководстве описано, как интегрировать Lynda.com с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1c8f-105">Интеграция Lynda.com с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1c8f-106">С помощью Azure AD вы можете контролировать доступ к Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="f1c8f-107">Вы можете включить автоматический вход пользователей в Lynda.com (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1c8f-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1c8f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1c8f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1c8f-110">Prerequisites</span></span>

<span data-ttu-id="f1c8f-111">Чтобы настроить интеграцию Azure AD с Lynda.com, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="f1c8f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f1c8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1c8f-113">подписка Lynda.com с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1c8f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1c8f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1c8f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1c8f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1c8f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f1c8f-118">Scenario description</span></span>
<span data-ttu-id="f1c8f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1c8f-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1c8f-121">Добавление Lynda.com из коллекции</span><span class="sxs-lookup"><span data-stu-id="f1c8f-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="f1c8f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="f1c8f-123">Добавление Lynda.com из коллекции</span><span class="sxs-lookup"><span data-stu-id="f1c8f-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="f1c8f-124">Чтобы настроить интеграцию Lynda.com с Azure AD, необходимо добавить Lynda.com из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1c8f-125">**Чтобы добавить Lynda.com из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f1c8f-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1c8f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1c8f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1c8f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f1c8f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f1c8f-133">В поле поиска введите **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-133">In the search box, type **Lynda.com**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="f1c8f-135">На панели результатов выберите **Lynda.com**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1c8f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c8f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1c8f-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lynda.com для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1c8f-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Lynda.com соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="f1c8f-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="f1c8f-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="f1c8f-142">Чтобы настроить и проверить единый вход в Azure AD в Lynda.com, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1c8f-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1c8f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1c8f-145">**[Создание тестового пользователя Lynda.com](#creating-a-lyndacom-test-user)** требуется для создания в Lynda.com пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1c8f-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1c8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1c8f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c8f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1c8f-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="f1c8f-150">**Чтобы настроить единый вход Azure AD в Lynda.com, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f1c8f-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="f1c8f-151">На портале Azure на странице интеграции с приложением **Lynda.com** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f1c8f-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="f1c8f-155">В разделе **Домены и URL-адреса Lynda.com** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f1c8f-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="f1c8f-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="f1c8f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1c8f-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-158">This value is not real.</span></span> <span data-ttu-id="f1c8f-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f1c8f-160">Чтобы получить их, обратитесь в [службу поддержки клиентов Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="f1c8f-161">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="f1c8f-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f1c8f-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1c8f-165">Чтобы настроить единый вход на стороне **Lynda.com**, нужно отправить скачанный **XML-файл метаданных** в [службу поддержки Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1c8f-166">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c8f-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1c8f-167">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f1c8f-169">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f1c8f-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1c8f-170">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1c8f-172">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1c8f-174">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1c8f-176">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1c8f-178">а.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-178">a.</span></span> <span data-ttu-id="f1c8f-179">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1c8f-180">b.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-180">b.</span></span> <span data-ttu-id="f1c8f-181">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1c8f-182">c.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-182">c.</span></span> <span data-ttu-id="f1c8f-183">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1c8f-184">d.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-184">d.</span></span> <span data-ttu-id="f1c8f-185">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="f1c8f-186">Создание тестового пользователя Lynda.com</span><span class="sxs-lookup"><span data-stu-id="f1c8f-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="f1c8f-187">Элемент действия для настройки подготовки пользователей в Lynda.com отсутствует.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="f1c8f-188">Когда назначенный пользователь пытается войти в Lynda.com с помощью панели доступа, Lynda.com проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="f1c8f-189">Если учетная запись пользователя отсутствует, Lynda.com автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="f1c8f-190">Вы можете использовать любые другие средства создания учетной записи пользователя Lynda.com или API, предоставляемые Lynda.com для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1c8f-191">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c8f-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1c8f-192">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f1c8f-194">**Чтобы назначить пользователя Britta Simon в Lynda.com, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="f1c8f-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="f1c8f-195">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f1c8f-197">В списке приложений выберите **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-197">In the applications list, select **Lynda.com**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="f1c8f-199">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f1c8f-201">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-201">Click **Add** button.</span></span> <span data-ttu-id="f1c8f-202">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f1c8f-204">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1c8f-205">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1c8f-206">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1c8f-207">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f1c8f-207">Testing single sign-on</span></span>

<span data-ttu-id="f1c8f-208">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="f1c8f-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f1c8f-209">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1c8f-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1c8f-210">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f1c8f-210">Additional resources</span></span>

* [<span data-ttu-id="f1c8f-211">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1c8f-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1c8f-212">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1c8f-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

