---
title: "Учебник. Интеграция Azure Active Directory с Insperity ExpensAble | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="b6a41-103">Учебник. Интеграция Azure Active Directory с Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="b6a41-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="b6a41-104">В этом учебнике описано, как интегрировать Insperity ExpensAble с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6a41-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6a41-105">Интеграция Azure AD с приложением Insperity ExpensAble обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b6a41-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6a41-106">С помощью Azure AD вы можете контролировать доступ к Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="b6a41-107">Вы можете включить автоматический вход пользователей в Insperity ExpensAble (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6a41-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6a41-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6a41-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6a41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6a41-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6a41-110">Prerequisites</span></span>

<span data-ttu-id="b6a41-111">Чтобы настроить интеграцию Azure AD с Insperity ExpensAble, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b6a41-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="b6a41-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b6a41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6a41-113">подписка Insperity ExpensAble с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6a41-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6a41-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b6a41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6a41-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b6a41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6a41-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b6a41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6a41-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6a41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6a41-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b6a41-118">Scenario description</span></span>
<span data-ttu-id="b6a41-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b6a41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6a41-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b6a41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6a41-121">Добавление Insperity ExpensAble из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6a41-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="b6a41-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6a41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="b6a41-123">Добавление Insperity ExpensAble из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6a41-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="b6a41-124">Чтобы настроить интеграцию Insperity ExpensAble с Azure AD, необходимо добавить Insperity ExpensAble из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b6a41-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6a41-125">**Чтобы добавить Insperity ExpensAble из коллекции, выполните указанные далее действия:**</span><span class="sxs-lookup"><span data-stu-id="b6a41-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6a41-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6a41-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6a41-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b6a41-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b6a41-133">В поле поиска введите **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="b6a41-135">В области результатов выберите **Insperity ExpensAble** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b6a41-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6a41-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6a41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6a41-138">В этом разделе описана настройка и проверка единого входа Azure AD в Insperity ExpensAble с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6a41-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b6a41-139">Для включения единого входа в Azure AD необходимо знать, какой пользователь в приложении Insperity ExpensAble соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6a41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="b6a41-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="b6a41-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6a41-142">Чтобы настроить и проверить единый вход Azure AD в Insperity ExpensAble, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b6a41-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6a41-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b6a41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6a41-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6a41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6a41-145">**[Создание тестового пользователя Insperity ExpensAble](#creating-an-insperity-expensable-test-user)** требуется для создания пользователя Britta Simon в Insperity ExpensAble, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6a41-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6a41-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6a41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6a41-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b6a41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6a41-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6a41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6a41-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="b6a41-150">**Чтобы настроить единый вход Azure AD в Insperity ExpensAble, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b6a41-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="b6a41-151">На портале Azure на странице интеграции с приложением **Insperity ExpensAble** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b6a41-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6a41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="b6a41-155">В разделе **Домены и URL-адреса приложения Insperity ExpensAble** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b6a41-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="b6a41-157">а.</span><span class="sxs-lookup"><span data-stu-id="b6a41-157">a.</span></span> <span data-ttu-id="b6a41-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="b6a41-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6a41-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="b6a41-159">This value is not real.</span></span> <span data-ttu-id="b6a41-160">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="b6a41-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b6a41-161">Для получения этого значения обратитесь в [службу поддержки клиентов Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="b6a41-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="b6a41-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6a41-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="b6a41-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b6a41-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6a41-166">В разделе **Конфигурация Insperity ExpensAble** щелкните **Настроить Insperity ExpensAble**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b6a41-167">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="b6a41-169">Чтобы настроить единый вход на стороне **Insperity ExpensAble**, нужно отправить скачанный **XML-файл метаданных**, **URL-адрес службы единого входа SAML** и **идентификатор сущности SAML** в [службу поддержки Insperity ExpensAble](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="b6a41-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="b6a41-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="b6a41-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b6a41-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b6a41-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6a41-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b6a41-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6a41-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b6a41-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6a41-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6a41-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6a41-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6a41-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b6a41-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b6a41-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6a41-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6a41-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6a41-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6a41-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6a41-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6a41-186">а.</span><span class="sxs-lookup"><span data-stu-id="b6a41-186">a.</span></span> <span data-ttu-id="b6a41-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6a41-188">b.</span><span class="sxs-lookup"><span data-stu-id="b6a41-188">b.</span></span> <span data-ttu-id="b6a41-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6a41-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6a41-190">c.</span><span class="sxs-lookup"><span data-stu-id="b6a41-190">c.</span></span> <span data-ttu-id="b6a41-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6a41-192">d.</span><span class="sxs-lookup"><span data-stu-id="b6a41-192">d.</span></span> <span data-ttu-id="b6a41-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="b6a41-194">Создание тестового пользователя Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="b6a41-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="b6a41-195">Цель этого раздела — создать пользователя с именем Britta Simon в Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="b6a41-196">Обратитесь в [службу поддержки Insperity ExpensAble](http://expensable.com/support/support-overview), чтобы добавить пользователей в учетную запись Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6a41-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6a41-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6a41-198">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b6a41-200">**Чтобы назначить пользователя Britta Simon в Insperity ExpensAble, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b6a41-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="b6a41-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b6a41-203">В списке приложений выберите **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="b6a41-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b6a41-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-207">Click **Add** button.</span></span> <span data-ttu-id="b6a41-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b6a41-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6a41-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6a41-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b6a41-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6a41-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b6a41-213">Testing single sign-on</span></span>

<span data-ttu-id="b6a41-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b6a41-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b6a41-215">Щелкнув элемент Insperity ExpensAble на панели доступа, вы автоматически войдете в приложение Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="b6a41-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="b6a41-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6a41-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6a41-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6a41-217">Additional resources</span></span>

* [<span data-ttu-id="b6a41-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6a41-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6a41-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6a41-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

