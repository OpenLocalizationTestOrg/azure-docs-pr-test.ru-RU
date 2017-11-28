---
title: "Учебник. Интеграция Azure Active Directory с Mindflash | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="cfd73-103">Руководство. Интеграция Azure Active Directory с Mindflash</span><span class="sxs-lookup"><span data-stu-id="cfd73-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="cfd73-104">В этом руководстве описано, как интегрировать Mindflash с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfd73-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfd73-105">Интеграция Azure AD с приложением Mindflash обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="cfd73-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cfd73-106">С помощью Azure AD вы можете контролировать доступ к Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="cfd73-107">Вы можете включить автоматический вход пользователей в Mindflash (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd73-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfd73-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cfd73-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cfd73-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfd73-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfd73-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cfd73-110">Prerequisites</span></span>

<span data-ttu-id="cfd73-111">Чтобы настроить интеграцию Azure AD с Mindflash, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="cfd73-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="cfd73-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cfd73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfd73-113">Подписка на Mindflash с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="cfd73-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfd73-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cfd73-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfd73-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="cfd73-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfd73-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cfd73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfd73-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfd73-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfd73-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cfd73-118">Scenario description</span></span>
<span data-ttu-id="cfd73-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cfd73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfd73-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="cfd73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfd73-121">Добавление Mindflash из коллекции.</span><span class="sxs-lookup"><span data-stu-id="cfd73-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="cfd73-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="cfd73-123">Добавление Mindflash из коллекции</span><span class="sxs-lookup"><span data-stu-id="cfd73-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="cfd73-124">Чтобы настроить интеграцию Mindflash с Azure AD, необходимо добавить Mindflash из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cfd73-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cfd73-125">**Чтобы добавить Mindflash из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="cfd73-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd73-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfd73-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cfd73-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cfd73-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cfd73-133">В поле поиска введите **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-133">In the search box, type **Mindflash**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="cfd73-135">На панели результатов выберите **Mindflash** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="cfd73-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfd73-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd73-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfd73-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Mindflash с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd73-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfd73-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="cfd73-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="cfd73-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cfd73-142">Чтобы настроить и проверить единый вход Azure AD в Mindflash, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="cfd73-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cfd73-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="cfd73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cfd73-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd73-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfd73-145">**[Создание тестового пользователя Mindflash](#creating-a-mindflash-test-user)** требуется для создания в Mindflash пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd73-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfd73-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfd73-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfd73-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cfd73-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfd73-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd73-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfd73-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="cfd73-150">**Чтобы настроить единый вход Azure AD в Mindflash, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="cfd73-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd73-151">На портале Azure на странице интеграции с приложением **Mindflash** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cfd73-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfd73-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="cfd73-155">В разделе **Домены и URL-адреса приложения Mindflash** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="cfd73-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="cfd73-157">а.</span><span class="sxs-lookup"><span data-stu-id="cfd73-157">a.</span></span> <span data-ttu-id="cfd73-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="cfd73-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="cfd73-159">b.</span><span class="sxs-lookup"><span data-stu-id="cfd73-159">b.</span></span> <span data-ttu-id="cfd73-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="cfd73-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cfd73-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cfd73-161">These values are not real.</span></span> <span data-ttu-id="cfd73-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="cfd73-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cfd73-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cfd73-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="cfd73-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="cfd73-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="cfd73-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="cfd73-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfd73-168">Чтобы настроить единый вход на стороне **Mindflash**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cfd73-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="cfd73-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="cfd73-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cfd73-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="cfd73-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cfd73-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="cfd73-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfd73-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd73-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfd73-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfd73-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cfd73-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cfd73-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd73-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfd73-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfd73-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfd73-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cfd73-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfd73-184">а.</span><span class="sxs-lookup"><span data-stu-id="cfd73-184">a.</span></span> <span data-ttu-id="cfd73-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfd73-186">b.</span><span class="sxs-lookup"><span data-stu-id="cfd73-186">b.</span></span> <span data-ttu-id="cfd73-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfd73-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfd73-188">c.</span><span class="sxs-lookup"><span data-stu-id="cfd73-188">c.</span></span> <span data-ttu-id="cfd73-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cfd73-190">d.</span><span class="sxs-lookup"><span data-stu-id="cfd73-190">d.</span></span> <span data-ttu-id="cfd73-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="cfd73-192">Создание тестового пользователя Mindflash</span><span class="sxs-lookup"><span data-stu-id="cfd73-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="cfd73-193">Чтобы разрешить пользователям Azure AD вход в Mindflash, они должны быть подготовлены для Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="cfd73-194">В случае с Mindflash подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="cfd73-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="cfd73-195">Чтобы подготовить учетные записи пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cfd73-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="cfd73-196">Выполните вход в **Mindflash** на веб-сайте компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="cfd73-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="cfd73-197">Перейдите в раздел **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="cfd73-198">![Управление пользователями](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="cfd73-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="cfd73-199">Нажмите кнопку **Add Users** (Добавить пользователей), а затем выберите **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="cfd73-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="cfd73-200">В разделе **Add New Users** (Добавление новых пользователей) введите соответствующие данные действующей учетной записи Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="cfd73-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="cfd73-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users") (Добавление новых пользователей)</span><span class="sxs-lookup"><span data-stu-id="cfd73-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="cfd73-202">а.</span><span class="sxs-lookup"><span data-stu-id="cfd73-202">a.</span></span> <span data-ttu-id="cfd73-203">В текстовое поле **First Name** (Имя) введите **имя пользователя**, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="cfd73-204">b.</span><span class="sxs-lookup"><span data-stu-id="cfd73-204">b.</span></span> <span data-ttu-id="cfd73-205">В текстовое поле **Last Name** (Фамилия) введите **фамилию**, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="cfd73-206">c.</span><span class="sxs-lookup"><span data-stu-id="cfd73-206">c.</span></span> <span data-ttu-id="cfd73-207">В текстовое поле **Email** (Адрес электронной почты) введите **адрес электронной почты** пользователя, например **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="cfd73-208">b.</span><span class="sxs-lookup"><span data-stu-id="cfd73-208">b.</span></span> <span data-ttu-id="cfd73-209">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="cfd73-210">Для подготовки учетных записей пользователей AAD можно использовать любые другие средства создания учетных записей Mindflash или API, предоставляемое Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cfd73-211">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfd73-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cfd73-212">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cfd73-214">**Чтобы назначить пользователя Britta Simon в Mindflash, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cfd73-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="cfd73-215">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cfd73-217">В списке приложений выберите **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-217">In the applications list, select **Mindflash**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="cfd73-219">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cfd73-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-221">Click **Add** button.</span></span> <span data-ttu-id="cfd73-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cfd73-224">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cfd73-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfd73-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cfd73-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfd73-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cfd73-227">Testing single sign-on</span></span>

<span data-ttu-id="cfd73-228">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="cfd73-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cfd73-229">Когда вы щелкните элемент Mindflash на панели доступа, должна появиться страница входа в приложение Mindflash.</span><span class="sxs-lookup"><span data-stu-id="cfd73-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="cfd73-230">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cfd73-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfd73-231">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cfd73-231">Additional resources</span></span>

* [<span data-ttu-id="cfd73-232">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfd73-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfd73-233">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cfd73-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

