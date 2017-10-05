---
title: "Руководство. Интеграция Azure Active Directory с CA PPM | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и CA PPM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 4ca9268c26f681fcc96955b6161fe4a119b2dcf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="896f5-103">Учебник. Интеграция Azure Active Directory с CA PPM</span><span class="sxs-lookup"><span data-stu-id="896f5-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="896f5-104">В этом учебнике описано, как интегрировать CA PPM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="896f5-104">In this tutorial, you learn how to integrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="896f5-105">Интеграция Azure AD с приложением CA PPM обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="896f5-105">Integrating CA PPM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="896f5-106">С помощью Azure AD вы можете контролировать доступ к CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-106">You can control in Azure AD who has access to CA PPM</span></span>
- <span data-ttu-id="896f5-107">Вы можете включить автоматический вход пользователей в CA PPM (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="896f5-107">You can enable your users to automatically get signed-on to CA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="896f5-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="896f5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="896f5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="896f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="896f5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="896f5-110">Prerequisites</span></span>

<span data-ttu-id="896f5-111">Чтобы настроить интеграцию Azure AD с CA PPM, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="896f5-111">To configure Azure AD integration with CA PPM, you need the following items:</span></span>

- <span data-ttu-id="896f5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="896f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="896f5-113">подписка CA PPM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="896f5-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="896f5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="896f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="896f5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="896f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="896f5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="896f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="896f5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="896f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="896f5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="896f5-118">Scenario description</span></span>
<span data-ttu-id="896f5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="896f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="896f5-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="896f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="896f5-121">Добавление CA PPM из коллекции</span><span class="sxs-lookup"><span data-stu-id="896f5-121">Adding CA PPM from the gallery</span></span>
2. <span data-ttu-id="896f5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="896f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-the-gallery"></a><span data-ttu-id="896f5-123">Добавление CA PPM из коллекции</span><span class="sxs-lookup"><span data-stu-id="896f5-123">Adding CA PPM from the gallery</span></span>
<span data-ttu-id="896f5-124">Чтобы настроить интеграцию CA PPM с Azure AD, необходимо добавить CA PPM из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="896f5-124">To configure the integration of CA PPM into Azure AD, you need to add CA PPM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="896f5-125">**Чтобы добавить CA PPM из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="896f5-125">**To add CA PPM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="896f5-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="896f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="896f5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="896f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="896f5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="896f5-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="896f5-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="896f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="896f5-133">В поле поиска введите **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="896f5-133">In the search box, type **CA PPM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="896f5-135">На панели результатов выберите **CA PPM** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="896f5-135">In the results panel, select **CA PPM**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="896f5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="896f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="896f5-138">В этом разделе описана настройка и проверка единого входа Azure AD в CA PPM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="896f5-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="896f5-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в CA PPM соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="896f5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CA PPM is to a user in Azure AD.</span></span> <span data-ttu-id="896f5-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-140">In other words, a link relationship between an Azure AD user and the related user in CA PPM needs to be established.</span></span>

<span data-ttu-id="896f5-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-141">In CA PPM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="896f5-142">Чтобы настроить и проверить единый вход Azure AD в CA PPM, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="896f5-142">To configure and test Azure AD single sign-on with CA PPM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="896f5-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="896f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="896f5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="896f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="896f5-145">**[Создание тестового пользователя CA PPM](#creating-a-ca-ppm-test-user)** нужно для того, чтобы в CA PPM также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="896f5-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - to have a counterpart of Britta Simon in CA PPM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="896f5-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="896f5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="896f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="896f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="896f5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="896f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="896f5-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="896f5-150">**Чтобы настроить единый вход Azure AD в CA PPM, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="896f5-150">**To configure Azure AD single sign-on with CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="896f5-151">На портале Azure на странице интеграции с приложением **CA PPM** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="896f5-151">In the Azure portal, on the **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="896f5-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="896f5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="896f5-155">В разделе **Домены и URL-адреса приложения CA PPM** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="896f5-155">On the **CA PPM Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="896f5-157">а.</span><span class="sxs-lookup"><span data-stu-id="896f5-157">a.</span></span> <span data-ttu-id="896f5-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="896f5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="896f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="896f5-159">b.</span></span> <span data-ttu-id="896f5-160">В текстовом поле **URL-адрес ответа** введите `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`.</span><span class="sxs-lookup"><span data-stu-id="896f5-160">In the **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="896f5-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="896f5-161">This value is not real.</span></span> <span data-ttu-id="896f5-162">Вместо него нужно указать фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="896f5-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="896f5-163">Чтобы получить это значение, обратитесь к [группе поддержки CA PPM](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="896f5-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) to get this value.</span></span>
 
4. <span data-ttu-id="896f5-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="896f5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="896f5-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="896f5-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="896f5-168">В разделе **Настройка CA PPM** щелкните **Настроить CA PPM**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="896f5-168">On the **CA PPM Configuration** section, click **Configure CA PPM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="896f5-169">Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="896f5-169">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="896f5-171">Для настройки единого входа на стороне **CA PPM** необходимо отправить скачанный **сертификат (Base64)** и **идентификатор сущности SAML** [группе поддержки CA PPM](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="896f5-171">To configure single sign-on on **CA PPM** side, you need to send the downloaded **Certificate(Base64)** and **SAML Entity ID** to [CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="896f5-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="896f5-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="896f5-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="896f5-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="896f5-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="896f5-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="896f5-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="896f5-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="896f5-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="896f5-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="896f5-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="896f5-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="896f5-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="896f5-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="896f5-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="896f5-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="896f5-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="896f5-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="896f5-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="896f5-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="896f5-187">а.</span><span class="sxs-lookup"><span data-stu-id="896f5-187">a.</span></span> <span data-ttu-id="896f5-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="896f5-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="896f5-189">b.</span><span class="sxs-lookup"><span data-stu-id="896f5-189">b.</span></span> <span data-ttu-id="896f5-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="896f5-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="896f5-191">c.</span><span class="sxs-lookup"><span data-stu-id="896f5-191">c.</span></span> <span data-ttu-id="896f5-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="896f5-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="896f5-193">d.</span><span class="sxs-lookup"><span data-stu-id="896f5-193">d.</span></span> <span data-ttu-id="896f5-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="896f5-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="896f5-195">Создание тестового пользователя CA PPM</span><span class="sxs-lookup"><span data-stu-id="896f5-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="896f5-196">В этом разделе описано, как создать пользователя Britta Simon в приложении CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="896f5-197">Обратитесь к [группе поддержки CA PPM](mailto:catechnicalsupport@ca.com), чтобы добавить пользователей на платформу CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) to add the users in the CA PPM platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="896f5-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="896f5-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="896f5-199">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CA PPM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="896f5-201">**Чтобы назначить пользователя Britta Simon в CA PPM, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="896f5-201">**To assign Britta Simon to CA PPM, perform the following steps:**</span></span>

1. <span data-ttu-id="896f5-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="896f5-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="896f5-204">В списке приложений выберите **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="896f5-204">In the applications list, select **CA PPM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="896f5-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="896f5-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="896f5-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="896f5-208">Click **Add** button.</span></span> <span data-ttu-id="896f5-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="896f5-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="896f5-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="896f5-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="896f5-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="896f5-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="896f5-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="896f5-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="896f5-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="896f5-214">Testing single sign-on</span></span>

<span data-ttu-id="896f5-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="896f5-215">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="896f5-216">Щелкнув элемент CA PPM на панели доступа, вы автоматически войдете в приложение CA PPM.</span><span class="sxs-lookup"><span data-stu-id="896f5-216">When you click the CA PPM tile in the Access Panel, you should get automatically signed-on to your CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="896f5-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="896f5-217">Additional resources</span></span>

* [<span data-ttu-id="896f5-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="896f5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="896f5-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="896f5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

