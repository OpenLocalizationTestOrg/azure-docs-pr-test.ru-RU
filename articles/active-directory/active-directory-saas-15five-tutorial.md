---
title: "Руководство по интеграции Azure Active Directory с 15Five | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="18f0a-103">Руководство. Интеграция Azure Active Directory с 15Five</span><span class="sxs-lookup"><span data-stu-id="18f0a-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="18f0a-104">В этом руководстве объясняется, как интегрировать 15Five с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18f0a-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18f0a-105">Интеграция Azure AD с приложением 15Five обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="18f0a-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="18f0a-106">С помощью Azure AD вы можете контролировать, у кого доступ к приложению 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="18f0a-107">Вы можете включить автоматический вход пользователей в 15Five (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f0a-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18f0a-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="18f0a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="18f0a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18f0a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18f0a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18f0a-110">Prerequisites</span></span>

<span data-ttu-id="18f0a-111">Чтобы настроить интеграцию Azure AD с 15Five, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="18f0a-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="18f0a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="18f0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18f0a-113">подписка 15Five с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="18f0a-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18f0a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="18f0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18f0a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="18f0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18f0a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="18f0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18f0a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18f0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18f0a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="18f0a-118">Scenario description</span></span>
<span data-ttu-id="18f0a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="18f0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18f0a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="18f0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18f0a-121">Добавление 15Five из коллекции.</span><span class="sxs-lookup"><span data-stu-id="18f0a-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="18f0a-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="18f0a-123">Добавление 15Five из коллекции</span><span class="sxs-lookup"><span data-stu-id="18f0a-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="18f0a-124">Чтобы настроить интеграцию приложения 15Five с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="18f0a-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="18f0a-125">**Добавление приложения 15Five из коллекции**</span><span class="sxs-lookup"><span data-stu-id="18f0a-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="18f0a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18f0a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="18f0a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="18f0a-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="18f0a-133">В поле поиска введите **15Five**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-133">In the search box, type **15Five**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="18f0a-135">В области результатов выберите **15Five** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="18f0a-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18f0a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18f0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18f0a-138">В этом разделе мы настроим и проверим единый вход Azure AD в 15Five с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18f0a-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18f0a-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в 15Five соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f0a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="18f0a-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="18f0a-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="18f0a-142">Чтобы настроить и проверить единый вход Azure AD в 15Five, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="18f0a-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="18f0a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="18f0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="18f0a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18f0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18f0a-145">**[Создание тестового пользователя 15Five](#creating-a-15five-test-user)** требуется для создания в 15Five пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f0a-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="18f0a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18f0a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18f0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="18f0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18f0a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18f0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18f0a-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="18f0a-150">**Настройка единого входа Azure AD в 15Five**</span><span class="sxs-lookup"><span data-stu-id="18f0a-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="18f0a-151">На портале Azure на странице интеграции с приложением **15Five** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="18f0a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="18f0a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="18f0a-155">В разделе **Домены и URL-адреса приложения 15Five** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="18f0a-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="18f0a-157">а.</span><span class="sxs-lookup"><span data-stu-id="18f0a-157">a.</span></span> <span data-ttu-id="18f0a-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="18f0a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="18f0a-159">b.</span><span class="sxs-lookup"><span data-stu-id="18f0a-159">b.</span></span> <span data-ttu-id="18f0a-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="18f0a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18f0a-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="18f0a-161">These values are not real.</span></span> <span data-ttu-id="18f0a-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="18f0a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="18f0a-163">Чтобы получить их, обратитесь в [службу поддержки клиентов 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="18f0a-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="18f0a-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="18f0a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="18f0a-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="18f0a-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18f0a-168">Чтобы настроить единый вход на стороне **15Five**, отправьте в [службу поддержки 15Five](https://www.15five.com/contact/) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="18f0a-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="18f0a-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="18f0a-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="18f0a-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="18f0a-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="18f0a-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18f0a-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="18f0a-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="18f0a-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18f0a-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="18f0a-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="18f0a-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="18f0a-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18f0a-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18f0a-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18f0a-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="18f0a-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18f0a-184">а.</span><span class="sxs-lookup"><span data-stu-id="18f0a-184">a.</span></span> <span data-ttu-id="18f0a-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18f0a-186">b.</span><span class="sxs-lookup"><span data-stu-id="18f0a-186">b.</span></span> <span data-ttu-id="18f0a-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18f0a-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18f0a-188">c.</span><span class="sxs-lookup"><span data-stu-id="18f0a-188">c.</span></span> <span data-ttu-id="18f0a-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="18f0a-190">d.</span><span class="sxs-lookup"><span data-stu-id="18f0a-190">d.</span></span> <span data-ttu-id="18f0a-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="18f0a-192">Создание тестового пользователя 15Five</span><span class="sxs-lookup"><span data-stu-id="18f0a-192">Creating a 15Five test user</span></span>

<span data-ttu-id="18f0a-193">Чтобы пользователи Azure AD могли входить в 15Five, они должны быть подготовлены в приложении 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="18f0a-194">Для 15Five эта подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="18f0a-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="18f0a-195">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="18f0a-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="18f0a-196">Выполните вход на корпоративном веб-сайте **15Five** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="18f0a-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="18f0a-197">Откройте страницу **Управление компанией**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="18f0a-198">![Управление компанией](./media/active-directory-saas-15five-tutorial/IC784675.png "Управление компанией")</span><span class="sxs-lookup"><span data-stu-id="18f0a-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="18f0a-199">Последовательно выберите пункты **People (Люди) \> Add People (Добавить людей)**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="18f0a-200">![Люди](./media/active-directory-saas-15five-tutorial/IC784676.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="18f0a-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="18f0a-201">В разделе «Добавить новых пользователей» выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="18f0a-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="18f0a-202">![Добавление нового пользователя](./media/active-directory-saas-15five-tutorial/IC784677.png "Добавление нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="18f0a-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="18f0a-203">а.</span><span class="sxs-lookup"><span data-stu-id="18f0a-203">a.</span></span> <span data-ttu-id="18f0a-204">В соответствующих текстовых полях введите **имя**, **фамилию**, **должность** и **адрес электронной почты** действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="18f0a-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="18f0a-205">b.</span><span class="sxs-lookup"><span data-stu-id="18f0a-205">b.</span></span> <span data-ttu-id="18f0a-206">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="18f0a-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="18f0a-207">Владелец учетной записи Azure AD получит сообщение электронной почты со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="18f0a-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="18f0a-208">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="18f0a-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="18f0a-209">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="18f0a-211">**Назначение пользователя Britta Simon приложению 15Five**</span><span class="sxs-lookup"><span data-stu-id="18f0a-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="18f0a-212">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="18f0a-214">В списке приложений выберите **15Five**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-214">In the applications list, select **15Five**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="18f0a-216">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="18f0a-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-218">Click **Add** button.</span></span> <span data-ttu-id="18f0a-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="18f0a-221">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="18f0a-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18f0a-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="18f0a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18f0a-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="18f0a-224">Testing single sign-on</span></span>

<span data-ttu-id="18f0a-225">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="18f0a-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="18f0a-226">Когда вы нажмете плитку 15Five на панели доступа, должна появиться страница входа в приложение 15Five.</span><span class="sxs-lookup"><span data-stu-id="18f0a-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="18f0a-227">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18f0a-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="18f0a-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="18f0a-228">Additional resources</span></span>

* [<span data-ttu-id="18f0a-229">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18f0a-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18f0a-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18f0a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

