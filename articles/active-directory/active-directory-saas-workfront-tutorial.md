---
title: "Руководство. Интеграция Azure Active Directory с Workfront | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="83058-103">Руководство. Интеграция Azure Active Directory с Workfront</span><span class="sxs-lookup"><span data-stu-id="83058-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="83058-104">В этом руководстве описано, как интегрировать Workfront с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83058-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83058-105">Интеграция приложения Workfront с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="83058-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83058-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="83058-107">Вы можете включить автоматический вход пользователей в Workfront (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83058-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83058-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83058-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83058-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83058-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83058-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83058-110">Prerequisites</span></span>

<span data-ttu-id="83058-111">Чтобы настроить интеграцию Azure AD с Workfront, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="83058-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="83058-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="83058-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83058-113">подписка Workfront с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="83058-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83058-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="83058-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83058-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="83058-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83058-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="83058-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83058-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83058-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83058-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="83058-118">Scenario description</span></span>
<span data-ttu-id="83058-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="83058-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83058-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="83058-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83058-121">Добавление Workfront из коллекции.</span><span class="sxs-lookup"><span data-stu-id="83058-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="83058-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83058-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="83058-123">Добавление Workfront из коллекции</span><span class="sxs-lookup"><span data-stu-id="83058-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="83058-124">Чтобы настроить интеграцию приложения Workfront с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="83058-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83058-125">**Добавление приложения Workfront из коллекции**</span><span class="sxs-lookup"><span data-stu-id="83058-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83058-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83058-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83058-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="83058-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83058-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83058-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="83058-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="83058-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="83058-133">В поле поиска введите **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="83058-133">In the search box, type **Workfront**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="83058-135">На панели результатов выберите **Workfront** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="83058-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83058-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83058-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83058-138">В этом разделе описана настройка и проверка единого входа Azure AD в Workfront с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83058-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83058-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в Workfront соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83058-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="83058-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="83058-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83058-142">Чтобы настроить и проверить единый вход Azure AD в Workfront, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="83058-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83058-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="83058-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83058-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83058-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83058-145">**[Создание тестового пользователя Workfront](#creating-a-workfront-test-user)** требуется для создания в Workfront пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83058-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83058-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83058-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83058-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="83058-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83058-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83058-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83058-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="83058-150">**Настройка единого входа Azure AD в Workfront**</span><span class="sxs-lookup"><span data-stu-id="83058-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="83058-151">На портале Azure на странице интеграции с приложением **Workfront** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="83058-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="83058-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="83058-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="83058-155">В разделе **Домены и URL-адреса приложения Workfront** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="83058-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="83058-157">а.</span><span class="sxs-lookup"><span data-stu-id="83058-157">a.</span></span> <span data-ttu-id="83058-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="83058-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="83058-159">b.</span><span class="sxs-lookup"><span data-stu-id="83058-159">b.</span></span> <span data-ttu-id="83058-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="83058-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83058-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="83058-161">These values are not real.</span></span> <span data-ttu-id="83058-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="83058-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83058-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Workfront](https://www.workfront.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="83058-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="83058-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="83058-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="83058-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="83058-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83058-168">В разделе **Настройка Workfront** щелкните **Настроить Workfront**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="83058-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="83058-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="83058-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="83058-171">Войдите на корпоративный сайт Workfront с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="83058-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="83058-172">Перейдите к **Настройке единого входа**.</span><span class="sxs-lookup"><span data-stu-id="83058-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="83058-173">В диалоговом окне **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="83058-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Настройка единого входа][23]
   
    <span data-ttu-id="83058-175">а.</span><span class="sxs-lookup"><span data-stu-id="83058-175">a.</span></span> <span data-ttu-id="83058-176">Для параметра **Тип** выберите значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="83058-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="83058-177">b.</span><span class="sxs-lookup"><span data-stu-id="83058-177">b.</span></span> <span data-ttu-id="83058-178">Выберите **идентификатор поставщика службы**.</span><span class="sxs-lookup"><span data-stu-id="83058-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="83058-179">c.</span><span class="sxs-lookup"><span data-stu-id="83058-179">c.</span></span> <span data-ttu-id="83058-180">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **Login Portal URL** (URL-адрес портала для входа).</span><span class="sxs-lookup"><span data-stu-id="83058-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="83058-181">г)</span><span class="sxs-lookup"><span data-stu-id="83058-181">d.</span></span> <span data-ttu-id="83058-182">Вставьте **URL-адрес службы единого выхода** в текстовое поле **Sign-Out URL** (URL-адрес выхода).</span><span class="sxs-lookup"><span data-stu-id="83058-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="83058-183">д.</span><span class="sxs-lookup"><span data-stu-id="83058-183">e.</span></span> <span data-ttu-id="83058-184">Вставьте **URL-адрес изменения пароля** в текстовое поле **Change Password URL** (URL-адрес изменения пароля).</span><span class="sxs-lookup"><span data-stu-id="83058-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="83058-185">f.</span><span class="sxs-lookup"><span data-stu-id="83058-185">f.</span></span> <span data-ttu-id="83058-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="83058-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="83058-187">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="83058-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83058-188">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="83058-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83058-189">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="83058-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83058-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="83058-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="83058-191">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83058-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="83058-193">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="83058-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83058-194">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83058-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83058-196">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="83058-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83058-198">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83058-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83058-200">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="83058-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83058-202">а.</span><span class="sxs-lookup"><span data-stu-id="83058-202">a.</span></span> <span data-ttu-id="83058-203">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83058-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83058-204">b.</span><span class="sxs-lookup"><span data-stu-id="83058-204">b.</span></span> <span data-ttu-id="83058-205">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83058-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83058-206">c.</span><span class="sxs-lookup"><span data-stu-id="83058-206">c.</span></span> <span data-ttu-id="83058-207">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="83058-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83058-208">d.</span><span class="sxs-lookup"><span data-stu-id="83058-208">d.</span></span> <span data-ttu-id="83058-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="83058-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="83058-210">Создание тестового пользователя Workfront</span><span class="sxs-lookup"><span data-stu-id="83058-210">Creating a Workfront test user</span></span>

<span data-ttu-id="83058-211">Цель этого раздела — создать пользователя с именем Britta Simon в Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="83058-212">**Чтобы создать пользователя с именем Britta Simon в Workfront, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="83058-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="83058-213">Войдите на корпоративный сайт Workfront с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="83058-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="83058-214">В верхнем меню щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="83058-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="83058-215">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="83058-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="83058-216">В диалоговом окне "Новый пользователь" выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="83058-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Workfront][21] 
   
    <span data-ttu-id="83058-218">а.</span><span class="sxs-lookup"><span data-stu-id="83058-218">a.</span></span> <span data-ttu-id="83058-219">В текстовое поле **First Name** (Имя) введите Britta.</span><span class="sxs-lookup"><span data-stu-id="83058-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="83058-220">b.</span><span class="sxs-lookup"><span data-stu-id="83058-220">b.</span></span> <span data-ttu-id="83058-221">В текстовое поле **Last Name** (Фамилия) введите Simon.</span><span class="sxs-lookup"><span data-stu-id="83058-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="83058-222">c.</span><span class="sxs-lookup"><span data-stu-id="83058-222">c.</span></span> <span data-ttu-id="83058-223">В текстовом поле **адрес электронной почты** введите адрес электронной почты пользователя Britta Simon в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83058-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="83058-224">d.</span><span class="sxs-lookup"><span data-stu-id="83058-224">d.</span></span> <span data-ttu-id="83058-225">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="83058-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83058-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="83058-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83058-227">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="83058-229">**Назначение пользователя Britta Simon приложению Workfront**</span><span class="sxs-lookup"><span data-stu-id="83058-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="83058-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83058-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="83058-232">В списке приложений выберите **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="83058-232">In the applications list, select **Workfront**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="83058-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="83058-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="83058-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83058-236">Click **Add** button.</span></span> <span data-ttu-id="83058-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="83058-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="83058-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83058-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83058-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="83058-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83058-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="83058-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83058-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="83058-242">Testing single sign-on</span></span>

<span data-ttu-id="83058-243">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="83058-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="83058-244">Когда вы нажмете плитку Workfront на панели доступа, должна появиться страница входа в приложение Workfront.</span><span class="sxs-lookup"><span data-stu-id="83058-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="83058-245">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="83058-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83058-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="83058-246">Additional resources</span></span>

* [<span data-ttu-id="83058-247">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83058-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83058-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83058-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

