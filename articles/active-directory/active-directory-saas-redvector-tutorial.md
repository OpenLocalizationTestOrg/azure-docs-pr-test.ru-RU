---
title: "Руководство по интеграции Azure Active Directory с RedVector | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в RedVector."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: d7aedd360ba1d4c11da210f8fae7be6035007c22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="33af3-103">Руководство. Интеграция Azure Active Directory с RedVector</span><span class="sxs-lookup"><span data-stu-id="33af3-103">Tutorial: Azure Active Directory integration with RedVector</span></span>

<span data-ttu-id="33af3-104">В этом руководстве описано, как интегрировать RedVector с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33af3-104">In this tutorial, you learn how to integrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33af3-105">Интеграция Azure AD с приложением RedVector обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="33af3-105">Integrating RedVector with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33af3-106">С помощью Azure AD вы можете контролировать доступ к RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-106">You can control in Azure AD who has access to RedVector</span></span>
- <span data-ttu-id="33af3-107">Вы можете включить автоматический вход пользователей в RedVector (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-107">You can enable your users to automatically get signed-on to RedVector (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33af3-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="33af3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33af3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33af3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33af3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33af3-110">Prerequisites</span></span>

<span data-ttu-id="33af3-111">Чтобы настроить интеграцию Azure AD с приложением RedVector, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="33af3-111">To configure Azure AD integration with RedVector, you need the following items:</span></span>

- <span data-ttu-id="33af3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="33af3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33af3-113">подписка RedVector с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="33af3-113">A RedVector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33af3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="33af3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33af3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="33af3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33af3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="33af3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33af3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33af3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33af3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="33af3-118">Scenario description</span></span>
<span data-ttu-id="33af3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="33af3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33af3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="33af3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33af3-121">Добавление RedVector из коллекции</span><span class="sxs-lookup"><span data-stu-id="33af3-121">Adding RedVector from the gallery</span></span>
2. <span data-ttu-id="33af3-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-redvector-from-the-gallery"></a><span data-ttu-id="33af3-123">Добавление RedVector из коллекции</span><span class="sxs-lookup"><span data-stu-id="33af3-123">Adding RedVector from the gallery</span></span>
<span data-ttu-id="33af3-124">Чтобы настроить интеграцию RedVector с Azure AD, необходимо добавить RedVector из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="33af3-124">To configure the integration of RedVector into Azure AD, you need to add RedVector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33af3-125">**Чтобы добавить RedVector из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="33af3-125">**To add RedVector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33af3-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33af3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33af3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="33af3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33af3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="33af3-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="33af3-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="33af3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="33af3-133">В поле поиска введите **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="33af3-133">In the search box, type **RedVector**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_search.png)

5. <span data-ttu-id="33af3-135">На панели результатов выберите **RedVector** и щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="33af3-135">In the results panel, select **RedVector**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33af3-137">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33af3-138">В этом разделе описана настройка и проверка единого входа Azure AD в RedVector с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33af3-138">In this section, you configure and test Azure AD single sign-on with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33af3-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в RedVector соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RedVector is to a user in Azure AD.</span></span> <span data-ttu-id="33af3-140">Иными словами, необходимо установить связь между пользователем Azure AD и его представлением в RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-140">In other words, a link relationship between an Azure AD user and the related user in RedVector needs to be established.</span></span>

<span data-ttu-id="33af3-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-141">In RedVector, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33af3-142">Чтобы настроить и проверить единый вход Azure AD в RedVector, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="33af3-142">To configure and test Azure AD single sign-on with RedVector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33af3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="33af3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33af3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33af3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33af3-145">**[Создание тестового пользователя RedVector](#creating-a-redvector-test-user)** требуется для создания пользователя Britta Simon в RedVector, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-145">**[Creating a RedVector test user](#creating-a-redvector-test-user)** - to have a counterpart of Britta Simon in RedVector that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="33af3-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33af3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33af3-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="33af3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33af3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="33af3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33af3-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RedVector application.</span></span>

<span data-ttu-id="33af3-150">**Чтобы настроить единый вход Azure AD в RedVector, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="33af3-150">**To configure Azure AD single sign-on with RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="33af3-151">На портале Azure на странице интеграции с приложением **RedVector** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="33af3-151">In the Azure portal, on the **RedVector** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="33af3-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="33af3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_samlbase.png)

3. <span data-ttu-id="33af3-155">В разделе **Домены и URL-адреса приложения RedVector** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="33af3-155">On the **RedVector Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_url.png)

    <span data-ttu-id="33af3-157">а.</span><span class="sxs-lookup"><span data-stu-id="33af3-157">a.</span></span> <span data-ttu-id="33af3-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://sso2.redvector.com/adfs/<Companyname>`</span><span class="sxs-lookup"><span data-stu-id="33af3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso2.redvector.com/adfs/<Companyname>`</span></span>

    <span data-ttu-id="33af3-159">b.</span><span class="sxs-lookup"><span data-stu-id="33af3-159">b.</span></span> <span data-ttu-id="33af3-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<Companyname>.redvector.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="33af3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Companyname>.redvector.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33af3-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="33af3-161">These values are not real.</span></span> <span data-ttu-id="33af3-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="33af3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="33af3-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="33af3-163">Contact [RedVector Client support team](mailto:sso@redvector.com) to get these values.</span></span> 
 
4. <span data-ttu-id="33af3-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="33af3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_certificate.png) 

5. <span data-ttu-id="33af3-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="33af3-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33af3-168">В разделе **Настройка RedVector** выберите **Настроить RedVector**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="33af3-168">On the **RedVector Configuration** section, click **Configure RedVector** to open **Configure sign-on** window.</span></span> <span data-ttu-id="33af3-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="33af3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_configure.png) 

7. <span data-ttu-id="33af3-171">Чтобы настроить единый вход на стороне **RedVector**, нужно отправить скачанный **сертификат (Base64)** и **URL-адрес службы единого входа SAML** в [службу поддержки RedVector](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="33af3-171">To configure single sign-on on **RedVector** side, you need to send the downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** to [RedVector support team](mailto:sso@redvector.com).</span></span> <span data-ttu-id="33af3-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="33af3-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="33af3-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="33af3-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33af3-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="33af3-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33af3-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="33af3-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33af3-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="33af3-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="33af3-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33af3-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="33af3-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="33af3-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33af3-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33af3-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33af3-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="33af3-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33af3-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="33af3-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33af3-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="33af3-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33af3-188">а.</span><span class="sxs-lookup"><span data-stu-id="33af3-188">a.</span></span> <span data-ttu-id="33af3-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33af3-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33af3-190">b.</span><span class="sxs-lookup"><span data-stu-id="33af3-190">b.</span></span> <span data-ttu-id="33af3-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="33af3-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33af3-192">c.</span><span class="sxs-lookup"><span data-stu-id="33af3-192">c.</span></span> <span data-ttu-id="33af3-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="33af3-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33af3-194">d.</span><span class="sxs-lookup"><span data-stu-id="33af3-194">d.</span></span> <span data-ttu-id="33af3-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="33af3-195">Click **Create**.</span></span>
 
### <a name="creating-a-redvector-test-user"></a><span data-ttu-id="33af3-196">Создание тестового пользователя RedVector</span><span class="sxs-lookup"><span data-stu-id="33af3-196">Creating a RedVector test user</span></span>

<span data-ttu-id="33af3-197">В этом разделе описано, как создать пользователя Britta Simon в приложении RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-197">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="33af3-198">Если вы не знаете, как добавить Britta Simon в RedVector, обратитесь в [службу поддержки RedVector](mailto:sso@redvector.com) с просьбой добавить тестового пользователя и включить единый вход.</span><span class="sxs-lookup"><span data-stu-id="33af3-198">If you don't know how to add Britta Simon in RedVector, Work with [RedVector support team](mailto:sso@redvector.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33af3-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="33af3-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33af3-200">В этом разделе описано, как предоставить пользователю Britta Simon доступ к RedVector, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="33af3-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RedVector.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="33af3-202">**Чтобы назначить пользователя Britta Simon в RedVector, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="33af3-202">**To assign Britta Simon to RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="33af3-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="33af3-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="33af3-205">В списке приложений выберите **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="33af3-205">In the applications list, select **RedVector**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_app.png) 

3. <span data-ttu-id="33af3-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="33af3-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="33af3-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="33af3-209">Click **Add** button.</span></span> <span data-ttu-id="33af3-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="33af3-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="33af3-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="33af3-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33af3-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="33af3-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33af3-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="33af3-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33af3-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="33af3-215">Testing single sign-on</span></span>

<span data-ttu-id="33af3-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="33af3-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="33af3-217">Щелкнув элемент RedVector на панели доступа, вы автоматически войдете в приложение RedVector.</span><span class="sxs-lookup"><span data-stu-id="33af3-217">When you click the RedVector tile in the Access Panel, you should get automatically signed-on to your RedVector application..</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33af3-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="33af3-218">Additional resources</span></span>

* [<span data-ttu-id="33af3-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33af3-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33af3-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33af3-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_203.png

