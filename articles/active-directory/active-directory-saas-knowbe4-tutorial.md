---
title: "Руководство по интеграции Azure Active Directory с KnowBe4 Security Awareness Training | Документация Майкрософт"
description: "Узнайте, как настраивать единый вход между Azure Active Directory и KnowBe4 Security Awareness Training."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="67845-103">Руководство по интеграции Azure Active Directory с KnowBe4 Security Awareness Training</span><span class="sxs-lookup"><span data-stu-id="67845-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="67845-104">В этом руководстве вы узнаете, как интегрировать KnowBe4 Security Awareness Training с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67845-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67845-105">Интеграция KnowBe4 Security Awareness Training с Azure AD предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="67845-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="67845-106">С помощью Azure AD вы можете контролировать доступ к KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="67845-107">Вы можете позволить пользователям автоматически входить в KnowBe4 Security Awareness Training (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67845-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67845-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="67845-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="67845-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67845-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67845-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67845-110">Prerequisites</span></span>

<span data-ttu-id="67845-111">Чтобы настроить интеграцию Azure AD с KnowBe4 Security Awareness Training, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="67845-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="67845-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="67845-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67845-113">подписка KnowBe4 Security Awareness Training с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="67845-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67845-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="67845-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67845-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="67845-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67845-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="67845-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67845-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67845-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67845-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="67845-118">Scenario description</span></span>
<span data-ttu-id="67845-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="67845-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67845-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="67845-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67845-121">Добавление KnowBe4 Security Awareness Training из коллекции.</span><span class="sxs-lookup"><span data-stu-id="67845-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="67845-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67845-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="67845-123">Добавление KnowBe4 Security Awareness Training из коллекции</span><span class="sxs-lookup"><span data-stu-id="67845-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="67845-124">Для настройки интеграции KnowBe4 Security Awareness Training с Azure AD необходимо добавить KnowBe4 Security Awareness Training из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="67845-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="67845-125">**Чтобы добавить KnowBe4 Security Awareness Training из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="67845-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="67845-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67845-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67845-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="67845-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="67845-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="67845-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="67845-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="67845-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="67845-133">В поле поиска введите **KnowBe4 Security Awareness Training**.</span><span class="sxs-lookup"><span data-stu-id="67845-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="67845-135">На панели результатов выберите **KnowBe4 Security Awareness Training** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="67845-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67845-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67845-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67845-138">В этом разделе описана настройка и проверка единого входа Azure AD в KnowBe4 Security Awareness Training с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67845-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="67845-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь KnowBe4 Security Awareness Training соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67845-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="67845-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="67845-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="67845-142">Чтобы настроить и проверить единый вход Azure AD в KnowBe4 Security Awareness Training, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="67845-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="67845-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="67845-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="67845-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67845-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67845-145">**[Создание тестового пользователя KnowBe4 Security Awareness Training](#creating-a-knowbe4-security-awareness-training-test-user)** требуется для создания пользователя Britta Simon в KnowBe4 Security Awareness Training, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67845-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="67845-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67845-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67845-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="67845-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67845-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="67845-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67845-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="67845-150">**Чтобы настроить единый вход Azure AD в KnowBe4 Security Awareness Training, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="67845-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="67845-151">На портале Azure на странице интеграции с приложением **KnowBe4 Security Awareness Training** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="67845-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="67845-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="67845-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="67845-155">В разделе **KnowBe4 Security Awareness Training** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="67845-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="67845-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="67845-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67845-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="67845-158">The value is not real.</span></span> <span data-ttu-id="67845-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="67845-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="67845-160">Обратитесь в [службу поддержки KnowBe4 Security Awareness Training Client](mailto:support@KnowBe4.com), чтобы получить значение.</span><span class="sxs-lookup"><span data-stu-id="67845-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="67845-161">В разделе **Сертификат подписи SAML** щелкните **Certificate (Raw)** (Сертификат (необработанный)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="67845-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="67845-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="67845-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67845-165">В разделе **Настройка KnowBe4 Security Awareness Training** щелкните **Настроить KnowBe4 Security Awareness Training**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="67845-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="67845-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="67845-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="67845-168">Чтобы настроить единый вход на стороне **KnowBe4 Security Awareness Training**, необходимо отправить скачанный **необработанный файл сертификата**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа** в [службу поддержки KnowBe4 Security Awareness Training](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="67845-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="67845-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="67845-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="67845-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="67845-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="67845-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="67845-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67845-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="67845-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="67845-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67845-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="67845-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="67845-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="67845-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="67845-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67845-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="67845-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67845-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="67845-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67845-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="67845-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67845-184">а.</span><span class="sxs-lookup"><span data-stu-id="67845-184">a.</span></span> <span data-ttu-id="67845-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67845-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67845-186">b.</span><span class="sxs-lookup"><span data-stu-id="67845-186">b.</span></span> <span data-ttu-id="67845-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67845-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67845-188">c.</span><span class="sxs-lookup"><span data-stu-id="67845-188">c.</span></span> <span data-ttu-id="67845-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="67845-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="67845-190">d.</span><span class="sxs-lookup"><span data-stu-id="67845-190">d.</span></span> <span data-ttu-id="67845-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="67845-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="67845-192">Создание тестового пользователя KnowBe4 Security Awareness Training</span><span class="sxs-lookup"><span data-stu-id="67845-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="67845-193">В этом разделе описано, как создать пользователя с именем Britta Simon в приложении KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="67845-194">Приложение KnowBe4 Security Awareness Training поддерживает JIT-подготовку, включенную по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="67845-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="67845-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="67845-195">There is no action item for you in this section.</span></span> <span data-ttu-id="67845-196">Новый пользователь будет создан при попытке получить доступ к приложению KnowBe4 Security Awareness Training (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="67845-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="67845-197">Если необходимо создать пользователя вручную, свяжитесь со [службой поддержки KnowBe4 Security Awareness Training](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="67845-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="67845-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="67845-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="67845-199">В этом разделе описано, как предоставить пользователю Britta Simon доступ к KnowBe4 Security Awareness Training, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="67845-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="67845-201">**Чтобы назначить пользователя Britta Simon в KnowBe4 Security Awareness Training, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="67845-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="67845-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="67845-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="67845-204">В списке приложений выберите **KnowBe4 Security Awareness Training**.</span><span class="sxs-lookup"><span data-stu-id="67845-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="67845-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="67845-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="67845-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="67845-208">Click **Add** button.</span></span> <span data-ttu-id="67845-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="67845-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="67845-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="67845-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="67845-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="67845-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67845-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="67845-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67845-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="67845-214">Testing single sign-on</span></span>

<span data-ttu-id="67845-215">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="67845-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="67845-216">Щелкнув панель KnowBe4 Security Awareness Training на панели доступа, вы автоматически войдете в приложение KnowBe4 Security Awareness Training.</span><span class="sxs-lookup"><span data-stu-id="67845-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67845-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="67845-217">Additional resources</span></span>

* [<span data-ttu-id="67845-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67845-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67845-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67845-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

