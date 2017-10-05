---
title: "Учебник. Интеграция Azure Active Directory с EmpCenter | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в EmpCenter."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: aa27175165f4b15477bef4e70ad1c25016db31a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="a8331-103">Руководство. Интеграция Azure Active Directory с EmpCenter</span><span class="sxs-lookup"><span data-stu-id="a8331-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="a8331-104">В этом руководстве описано, как интегрировать EmpCenter с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8331-104">In this tutorial, you learn how to integrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8331-105">Интеграция Azure AD с приложением EmpCenter обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="a8331-105">Integrating EmpCenter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8331-106">С помощью Azure AD вы можете контролировать доступ к EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-106">You can control in Azure AD who has access to EmpCenter</span></span>
- <span data-ttu-id="a8331-107">Вы можете включить автоматический вход пользователей в EmpCenter (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8331-107">You can enable your users to automatically get signed-on to EmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8331-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a8331-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8331-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8331-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8331-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8331-110">Prerequisites</span></span>

<span data-ttu-id="a8331-111">Чтобы настроить интеграцию Azure AD с EmpCenter, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a8331-111">To configure Azure AD integration with EmpCenter, you need the following items:</span></span>

- <span data-ttu-id="a8331-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a8331-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8331-113">Подписка с поддержкой единого входа EmpCenter</span><span class="sxs-lookup"><span data-stu-id="a8331-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8331-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a8331-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8331-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a8331-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8331-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a8331-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8331-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8331-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8331-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a8331-118">Scenario description</span></span>
<span data-ttu-id="a8331-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a8331-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8331-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a8331-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8331-121">Добавление EmpCenter из коллекции</span><span class="sxs-lookup"><span data-stu-id="a8331-121">Adding EmpCenter from the gallery</span></span>
2. <span data-ttu-id="a8331-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8331-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-the-gallery"></a><span data-ttu-id="a8331-123">Добавление EmpCenter из коллекции</span><span class="sxs-lookup"><span data-stu-id="a8331-123">Adding EmpCenter from the gallery</span></span>
<span data-ttu-id="a8331-124">Чтобы настроить интеграцию EmpCenter с Azure AD, необходимо добавить EmpCenter из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a8331-124">To configure the integration of EmpCenter into Azure AD, you need to add EmpCenter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8331-125">**Чтобы добавить EmpCenter из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="a8331-125">**To add EmpCenter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8331-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8331-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8331-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8331-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8331-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8331-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a8331-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a8331-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a8331-133">В поле поиска введите **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="a8331-133">In the search box, type **EmpCenter**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="a8331-135">На панели результатов выберите **EmpCenter** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a8331-135">In the results panel, select **EmpCenter**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8331-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8331-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8331-138">В этом разделе описана настройка и проверка единого входа Azure AD в EmpCenter с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8331-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a8331-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в EmpCenter соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8331-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EmpCenter is to a user in Azure AD.</span></span> <span data-ttu-id="a8331-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-140">In other words, a link relationship between an Azure AD user and the related user in EmpCenter needs to be established.</span></span>

<span data-ttu-id="a8331-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-141">In EmpCenter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8331-142">Чтобы настроить и проверить единый вход Azure AD в EmpCenter, вам потребуется выполнить действия в перечисленных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a8331-142">To configure and test Azure AD single sign-on with EmpCenter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8331-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a8331-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8331-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8331-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8331-145">**[Создание тестового пользователя EmpCenter](#creating-an-empcenter-test-user)** требуется для создания пользователя Britta Simon в EmpCenter, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8331-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - to have a counterpart of Britta Simon in EmpCenter that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8331-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8331-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8331-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8331-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8331-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8331-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8331-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="a8331-150">**Чтобы настроить единый вход Azure AD в EmpCenter, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="a8331-150">**To configure Azure AD single sign-on with EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="a8331-151">На портале Azure на странице интеграции с приложением **EmpCenter** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a8331-151">In the Azure portal, on the **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a8331-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8331-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="a8331-155">В разделе **Домены и URL-адреса приложения EmpCenter** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a8331-155">On the **EmpCenter Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="a8331-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="a8331-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="a8331-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="a8331-158">The value is not real.</span></span> <span data-ttu-id="a8331-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a8331-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a8331-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="a8331-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) to get the value.</span></span> 
 
4. <span data-ttu-id="a8331-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8331-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="a8331-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a8331-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8331-165">Чтобы настроить единый вход на стороне **EmpCenter**, отправьте в [службу поддержки EmpCenter](http://www.workforcesoftware.com/services/customer-support/) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="a8331-165">To configure single sign-on on **EmpCenter** side, you need to send the downloaded **Metadata XML** to [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="a8331-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="a8331-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a8331-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a8331-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8331-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a8331-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8331-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a8331-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8331-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8331-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8331-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8331-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a8331-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a8331-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8331-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8331-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8331-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a8331-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8331-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8331-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8331-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8331-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8331-182">а.</span><span class="sxs-lookup"><span data-stu-id="a8331-182">a.</span></span> <span data-ttu-id="a8331-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8331-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8331-184">b.</span><span class="sxs-lookup"><span data-stu-id="a8331-184">b.</span></span> <span data-ttu-id="a8331-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8331-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8331-186">c.</span><span class="sxs-lookup"><span data-stu-id="a8331-186">c.</span></span> <span data-ttu-id="a8331-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a8331-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8331-188">d.</span><span class="sxs-lookup"><span data-stu-id="a8331-188">d.</span></span> <span data-ttu-id="a8331-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8331-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="a8331-190">Создание тестового пользователя EmpCenter</span><span class="sxs-lookup"><span data-stu-id="a8331-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="a8331-191">Чтобы пользователи Azure AD могли выполнять вход в EmpCenter, они должны быть подготовлены в EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-191">In order to enable Azure AD users to log in to EmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="a8331-192">В случае EmpCenter учетные записи пользователей должны быть созданы [службой поддержки EmpCenter](http://www.workforcesoftware.com/services/customer-support/).</span><span class="sxs-lookup"><span data-stu-id="a8331-192">In the case of EmpCenter, the user accounts need to be created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="a8331-193">Вы можете использовать любые другие инструменты создания учетных записей пользователя EmpCenter или API, предоставляемые EmpCenter для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8331-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8331-194">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8331-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8331-195">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EmpCenter.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a8331-197">**Чтобы назначить пользователя Britta Simon приложению EmpCenter, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="a8331-197">**To assign Britta Simon to EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="a8331-198">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8331-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a8331-200">В списке приложений выберите **EmpCenter**.</span><span class="sxs-lookup"><span data-stu-id="a8331-200">In the applications list, select **EmpCenter**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="a8331-202">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8331-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a8331-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8331-204">Click **Add** button.</span></span> <span data-ttu-id="a8331-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8331-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a8331-207">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a8331-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8331-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a8331-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8331-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a8331-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8331-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a8331-210">Testing single sign-on</span></span>


<span data-ttu-id="a8331-211">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a8331-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8331-212">Щелкнув плитку EmpCenter на панели доступа, вы автоматически войдете в приложение EmpCenter.</span><span class="sxs-lookup"><span data-stu-id="a8331-212">When you click the EmpCenter tile in the Access Panel, you should get automatically signed-on to your EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8331-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8331-213">Additional resources</span></span>

* [<span data-ttu-id="a8331-214">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8331-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8331-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8331-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png

