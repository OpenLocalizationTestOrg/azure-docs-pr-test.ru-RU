---
title: "Руководство по интеграции Azure Active Directory с Inkling | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="cac0d-103">Руководство по интеграции Azure Active Directory с Inkling</span><span class="sxs-lookup"><span data-stu-id="cac0d-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="cac0d-104">В этом руководстве описано, как интегрировать приложение Inkling с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cac0d-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cac0d-105">Интеграция Azure AD с приложением Inkling обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="cac0d-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cac0d-106">С помощью Azure AD вы можете контролировать доступ к Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="cac0d-107">Вы можете включить автоматический вход пользователей в Inkling (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cac0d-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cac0d-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="cac0d-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="cac0d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cac0d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cac0d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cac0d-110">Prerequisites</span></span>

<span data-ttu-id="cac0d-111">Чтобы настроить интеграцию Azure AD с Inkling, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="cac0d-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="cac0d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cac0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cac0d-113">подписка Inkling с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="cac0d-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="cac0d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cac0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cac0d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="cac0d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cac0d-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="cac0d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cac0d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cac0d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cac0d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cac0d-118">Scenario description</span></span>
<span data-ttu-id="cac0d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cac0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cac0d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="cac0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cac0d-121">Добавление Inkling из коллекции</span><span class="sxs-lookup"><span data-stu-id="cac0d-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="cac0d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac0d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="cac0d-123">Добавление Inkling из коллекции</span><span class="sxs-lookup"><span data-stu-id="cac0d-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="cac0d-124">Чтобы настроить интеграцию Inkling с Azure AD, необходимо добавить Inkling из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cac0d-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cac0d-125">**Чтобы добавить Inkling из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cac0d-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cac0d-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cac0d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cac0d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cac0d-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="cac0d-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cac0d-133">В поле поиска введите **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-133">In the search box, type **Inkling**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="cac0d-135">На панели результатов выберите **Inkling** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="cac0d-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cac0d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac0d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cac0d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Inkling с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cac0d-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cac0d-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Inkling соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cac0d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="cac0d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="cac0d-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="cac0d-142">Чтобы настроить и проверить единый вход Azure AD в Inkling, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="cac0d-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cac0d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="cac0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cac0d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cac0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cac0d-145">**[Создание тестового пользователя Inkling](#creating-an-inkling-test-user)** требуется для создания в Inkling пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cac0d-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="cac0d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cac0d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cac0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cac0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cac0d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cac0d-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="cac0d-150">**Чтобы настроить единый вход Azure AD в Inkling, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cac0d-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="cac0d-151">На портале управления Azure на странице интеграции с приложением **Inkling** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cac0d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="cac0d-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="cac0d-155">В разделе **Домены и URL-адреса приложения Inkling** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cac0d-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="cac0d-157">а.</span><span class="sxs-lookup"><span data-stu-id="cac0d-157">a.</span></span> <span data-ttu-id="cac0d-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="cac0d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="cac0d-159">b.</span><span class="sxs-lookup"><span data-stu-id="cac0d-159">b.</span></span> <span data-ttu-id="cac0d-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://api.inkling.com/saml/v2/acs/<user-id>`.</span><span class="sxs-lookup"><span data-stu-id="cac0d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cac0d-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cac0d-161">Please note that these are not the real values.</span></span> <span data-ttu-id="cac0d-162">Необходимо указать фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="cac0d-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="cac0d-163">Чтобы получить эти значения, обратитесь в [службу поддержки Inkling](mailto:press@inkling.com).</span><span class="sxs-lookup"><span data-stu-id="cac0d-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="cac0d-164">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="cac0d-166">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите **дату окончания срока действия**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="cac0d-167">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-167">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="cac0d-169">В разделе **Сертификат подписи SAML** выберите **Make new certificate active** (Сделать новый сертификат активным) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="cac0d-171">Во всплывающем окне **Rollover certificate** (Сертификат восстановления) нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="cac0d-173">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="cac0d-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="cac0d-175">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки Inkling](mailto:press@inkling.com) и предоставьте скачанный **файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cac0d-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac0d-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="cac0d-177">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cac0d-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cac0d-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cac0d-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cac0d-180">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cac0d-182">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="cac0d-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cac0d-184">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cac0d-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cac0d-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cac0d-188">а.</span><span class="sxs-lookup"><span data-stu-id="cac0d-188">a.</span></span> <span data-ttu-id="cac0d-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cac0d-190">b.</span><span class="sxs-lookup"><span data-stu-id="cac0d-190">b.</span></span> <span data-ttu-id="cac0d-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cac0d-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cac0d-192">c.</span><span class="sxs-lookup"><span data-stu-id="cac0d-192">c.</span></span> <span data-ttu-id="cac0d-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cac0d-194">d.</span><span class="sxs-lookup"><span data-stu-id="cac0d-194">d.</span></span> <span data-ttu-id="cac0d-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="cac0d-196">Создание тестового пользователя Inkling</span><span class="sxs-lookup"><span data-stu-id="cac0d-196">Creating an Inkling test user</span></span>

<span data-ttu-id="cac0d-197">В этом разделе описано, как создать пользователя Britta Simon в приложении Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="cac0d-198">Обратитесь в [службу поддержки Inkling](mailto:press@inkling.com), чтобы добавить пользователей на платформу Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cac0d-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cac0d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cac0d-200">Цель этого раздела — разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cac0d-202">**Чтобы назначить пользователя Britta Simon приложению Inkling, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cac0d-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="cac0d-203">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cac0d-205">В списке приложений выберите **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-205">In the applications list, select **Inkling**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="cac0d-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cac0d-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-209">Click **Add** button.</span></span> <span data-ttu-id="cac0d-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cac0d-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cac0d-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cac0d-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cac0d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="cac0d-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cac0d-215">Testing single sign-on</span></span>

<span data-ttu-id="cac0d-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="cac0d-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cac0d-217">Щелкнув элемент Inkling на панели доступа, вы автоматически войдете в приложение Inkling.</span><span class="sxs-lookup"><span data-stu-id="cac0d-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cac0d-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cac0d-218">Additional resources</span></span>

* [<span data-ttu-id="cac0d-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cac0d-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cac0d-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cac0d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png