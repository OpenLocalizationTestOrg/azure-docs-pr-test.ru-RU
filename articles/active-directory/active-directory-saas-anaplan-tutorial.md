---
title: "Руководство. Интеграция Azure Active Directory с Anaplan | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Anaplan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: c2ecfd5f066ed3bd10f74f935de2f2b80057329f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="a3cfd-103">Руководство. Интеграция Azure Active Directory с Anaplan</span><span class="sxs-lookup"><span data-stu-id="a3cfd-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="a3cfd-104">В этом руководстве описано, как интегрировать Anaplan с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3cfd-105">Интеграция Azure AD с приложением Anaplan обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a3cfd-106">С помощью Azure AD вы можете контролировать доступ к Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-106">You can control in Azure AD who has access to Anaplan</span></span>
- <span data-ttu-id="a3cfd-107">Вы можете включить автоматический вход пользователей в Anaplan (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3cfd-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a3cfd-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3cfd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a3cfd-110">Prerequisites</span></span>

<span data-ttu-id="a3cfd-111">Чтобы настроить интеграцию Azure AD с Anaplan, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a3cfd-111">To configure Azure AD integration with Anaplan, you need the following items:</span></span>

- <span data-ttu-id="a3cfd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a3cfd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3cfd-113">подписка Anaplan с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3cfd-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3cfd-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a3cfd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3cfd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3cfd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3cfd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a3cfd-118">Scenario description</span></span>
<span data-ttu-id="a3cfd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3cfd-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a3cfd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3cfd-121">Добавление Anaplan из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-121">Adding Anaplan from the gallery</span></span>
2. <span data-ttu-id="a3cfd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cfd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-the-gallery"></a><span data-ttu-id="a3cfd-123">Добавление Anaplan из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-123">Adding Anaplan from the gallery</span></span>
<span data-ttu-id="a3cfd-124">Чтобы настроить интеграцию Anaplan с Azure AD, необходимо добавить Anaplan из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3cfd-125">**Чтобы добавить Anaplan из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a3cfd-125">**To add Anaplan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3cfd-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3cfd-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a3cfd-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a3cfd-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a3cfd-133">В поле поиска введите **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-133">In the search box, type **Anaplan**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="a3cfd-135">На панели результатов выберите **Anaplan** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3cfd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cfd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3cfd-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Anaplan с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a3cfd-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Anaplan соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span></span> <span data-ttu-id="a3cfd-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span></span>

<span data-ttu-id="a3cfd-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a3cfd-142">Чтобы настроить и проверить единый вход Azure AD в Anaplan, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3cfd-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a3cfd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3cfd-145">**[Создание тестового пользователя Anaplan](#creating-an-anaplan-test-user)** нужно для того, чтобы в Anaplan также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3cfd-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3cfd-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3cfd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cfd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3cfd-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="a3cfd-150">**Чтобы настроить единый вход Azure AD в Anaplan, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a3cfd-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="a3cfd-151">На портале Azure на странице интеграции с приложением **Anaplan** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a3cfd-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="a3cfd-155">В разделе **Домены и URL-адреса приложения Anaplan** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="a3cfd-157">а.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-157">a.</span></span> <span data-ttu-id="a3cfd-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="a3cfd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="a3cfd-159">b.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-159">b.</span></span> <span data-ttu-id="a3cfd-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="a3cfd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a3cfd-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-161">These values are not real.</span></span> <span data-ttu-id="a3cfd-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a3cfd-163">Чтобы получить эти значения, обратитесь к [группе поддержки Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a3cfd-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="a3cfd-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a3cfd-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a3cfd-168">В разделе **Конфигурация Anaplan** щелкните **Настроить Anaplan**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a3cfd-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="a3cfd-171">Чтобы настроить единый вход на стороне **Anaplan**, нужно отправить скачанный **XML-файл метаданных**, **идентификатор сущности SAML**, **URL-адрес службы единого входа SAML** и **URL-адрес выхода** [группе поддержки Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="a3cfd-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a3cfd-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a3cfd-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a3cfd-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3cfd-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cfd-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3cfd-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a3cfd-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a3cfd-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3cfd-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3cfd-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3cfd-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3cfd-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3cfd-188">а.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-188">a.</span></span> <span data-ttu-id="a3cfd-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3cfd-190">b.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-190">b.</span></span> <span data-ttu-id="a3cfd-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3cfd-192">c.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-192">c.</span></span> <span data-ttu-id="a3cfd-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a3cfd-194">d.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-194">d.</span></span> <span data-ttu-id="a3cfd-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="a3cfd-196">Создание тестового пользователя Anaplan</span><span class="sxs-lookup"><span data-stu-id="a3cfd-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="a3cfd-197">В этом разделе описано, как создать пользователя Britta Simon в приложении Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="a3cfd-198">Обратитесь к [группе поддержки Anaplan](mailto:support@anaplan.com), чтобы добавить пользователей на платформу Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a3cfd-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3cfd-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a3cfd-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a3cfd-202">**Чтобы назначить пользователя Britta Simon в Anaplan, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a3cfd-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="a3cfd-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a3cfd-205">В списке приложений выберите **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-205">In the applications list, select **Anaplan**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="a3cfd-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a3cfd-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-209">Click **Add** button.</span></span> <span data-ttu-id="a3cfd-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a3cfd-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a3cfd-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3cfd-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3cfd-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a3cfd-215">Testing single sign-on</span></span>

<span data-ttu-id="a3cfd-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a3cfd-217">Щелкнув элемент Anaplan на панели доступа, вы автоматически войдете в приложение Anaplan.</span><span class="sxs-lookup"><span data-stu-id="a3cfd-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span></span>

<span data-ttu-id="a3cfd-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a3cfd-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a3cfd-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a3cfd-219">Additional resources</span></span>

* [<span data-ttu-id="a3cfd-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3cfd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3cfd-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3cfd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

