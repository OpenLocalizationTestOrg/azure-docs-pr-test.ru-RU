---
title: "Руководство по интеграции Azure Active Directory с Land Gorilla Client | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Land Gorilla."
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="8a9a3-103">Руководство по интеграции Azure Active Directory с Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="8a9a3-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="8a9a3-104">В этом руководстве описано, как интегрировать приложение Land Gorilla Client с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a9a3-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a9a3-105">Интеграция Azure AD с Land Gorilla Client обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a9a3-106">С помощью Azure AD вы можете контролировать доступ к Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="8a9a3-107">Вы можете включить автоматический вход пользователей в Land Gorilla Client (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a9a3-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="8a9a3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a9a3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8a9a3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a9a3-110">Prerequisites</span></span>

<span data-ttu-id="8a9a3-111">Чтобы настроить интеграцию Azure AD с Land Gorilla Client, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="8a9a3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8a9a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a9a3-113">подписка Land Gorilla Client с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="8a9a3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="8a9a3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a9a3-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8a9a3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a9a3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8a9a3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8a9a3-118">Scenario description</span></span>
<span data-ttu-id="8a9a3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a9a3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a9a3-121">Добавление Land Gorilla Client из коллекции</span><span class="sxs-lookup"><span data-stu-id="8a9a3-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="8a9a3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9a3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="8a9a3-123">Добавление Land Gorilla Client из коллекции</span><span class="sxs-lookup"><span data-stu-id="8a9a3-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="8a9a3-124">Чтобы настроить интеграцию Land Gorilla Client с Azure AD, необходимо добавить Land Gorilla Client из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a9a3-125">**Чтобы добавить Land Gorilla Client из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8a9a3-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9a3-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a9a3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a9a3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8a9a3-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8a9a3-133">В поле поиска введите **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="8a9a3-135">На панели результатов выберите **Land Gorilla Client** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a9a3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a9a3-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Land Gorilla Client с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a9a3-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Land Gorilla Client соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="8a9a3-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="8a9a3-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="8a9a3-142">Чтобы настроить и проверить единый вход Azure AD в Land Gorilla Client, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a9a3-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a9a3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD с ограниченной группой.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="8a9a3-145">**[Создание тестового пользователя Land Gorilla](#creating-a-land-gorilla-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="8a9a3-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a9a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a9a3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a9a3-149">В этом разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="8a9a3-150">**Чтобы настроить единый вход Azure AD в Land Gorilla Client, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8a9a3-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9a3-151">На портале управления Azure на странице интеграции с приложением **Land Gorilla Client** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8a9a3-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="8a9a3-155">В разделе **Домены и URL-адреса приложения Land Gorilla Client** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="8a9a3-157">А.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-157">a.</span></span> <span data-ttu-id="8a9a3-158">В текстовом поле **Идентификатор** введите значение, используя один из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="8a9a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-159">b.</span></span> <span data-ttu-id="8a9a3-160">В текстовое поле **URL-адрес ответа** введите URL-адрес, используя один из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="8a9a3-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="8a9a3-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-161">Please note that these are not the real values.</span></span> <span data-ttu-id="8a9a3-162">Необходимо указать фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8a9a3-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="8a9a3-164">Чтобы получить эти значения, обратитесь в [службу поддержки Land Gorilla Client](https://www.landgorilla.com/support/).</span><span class="sxs-lookup"><span data-stu-id="8a9a3-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="8a9a3-165">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="8a9a3-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8a9a3-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="8a9a3-169">Чтобы настроить единый вход для своего приложения на стороне Land Gorilla, обратитесь в [службу поддержки Land Gorilla Client](https://www.landgorilla.com/support/) и предоставьте скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a9a3-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9a3-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a9a3-171">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8a9a3-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8a9a3-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9a3-174">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a9a3-176">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a9a3-178">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a9a3-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a9a3-182">а.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-182">a.</span></span> <span data-ttu-id="8a9a3-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a9a3-184">b.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-184">b.</span></span> <span data-ttu-id="8a9a3-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a9a3-186">c.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-186">c.</span></span> <span data-ttu-id="8a9a3-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a9a3-188">d.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-188">d.</span></span> <span data-ttu-id="8a9a3-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="8a9a3-190">Создание тестового пользователя Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="8a9a3-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="8a9a3-191">Обратитесь в [службу поддержки Land Gorilla](https://www.landgorilla.com/support/), чтобы добавить пользователей на платформу Land Gorilla.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a9a3-192">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a9a3-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a9a3-193">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8a9a3-195">**Чтобы назначить пользователя Britta Simon в Land Gorilla Client, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8a9a3-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="8a9a3-196">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8a9a3-198">В списке приложений выберите **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="8a9a3-200">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8a9a3-202">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-202">Click **Add** button.</span></span> <span data-ttu-id="8a9a3-203">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8a9a3-205">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a9a3-206">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a9a3-207">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="8a9a3-208">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8a9a3-208">Testing single sign-on</span></span>

<span data-ttu-id="8a9a3-209">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a9a3-210">Щелкнув элемент Land Gorilla Client на панели доступа, вы автоматически войдете в приложение Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="8a9a3-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8a9a3-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8a9a3-211">Additional resources</span></span>

* [<span data-ttu-id="8a9a3-212">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a9a3-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a9a3-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a9a3-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
