---
title: "Руководство по интеграции Azure Active Directory с Trakopolis | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3887cf8c085c30eb01ac769944da2fcfe3df81f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="1dab2-103">Учебник. Интеграция Azure Active Directory с Trakopolis</span><span class="sxs-lookup"><span data-stu-id="1dab2-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="1dab2-104">В этом учебнике описано, как интегрировать приложение Trakopolis с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1dab2-104">In this tutorial, you learn how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dab2-105">Интеграция Azure AD с приложением Trakopolis обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="1dab2-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1dab2-106">Вы можете контролировать доступ к Trakopolis с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dab2-106">You can control in Azure AD who has access to Trakopolis</span></span>
- <span data-ttu-id="1dab2-107">Вы можете включить автоматический вход пользователей в Trakopolis с учетной записью Azure AD (единый вход).</span><span class="sxs-lookup"><span data-stu-id="1dab2-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dab2-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1dab2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1dab2-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1dab2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dab2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1dab2-110">Prerequisites</span></span>

<span data-ttu-id="1dab2-111">Чтобы настроить интеграцию Azure AD с Trakopolis, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1dab2-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

- <span data-ttu-id="1dab2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1dab2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dab2-113">подписка Trakopolis с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1dab2-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dab2-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="1dab2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dab2-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="1dab2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dab2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1dab2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dab2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dab2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dab2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1dab2-118">Scenario description</span></span>
<span data-ttu-id="1dab2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1dab2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dab2-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="1dab2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dab2-121">Добавление Trakopolis из коллекции</span><span class="sxs-lookup"><span data-stu-id="1dab2-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="1dab2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="1dab2-123">Добавление Trakopolis из коллекции</span><span class="sxs-lookup"><span data-stu-id="1dab2-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="1dab2-124">Чтобы настроить интеграцию Trakopolis с Azure AD, необходимо добавить Trakopolis из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1dab2-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1dab2-125">**Чтобы добавить Trakopolis из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1dab2-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1dab2-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dab2-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1dab2-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1dab2-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1dab2-133">В поле поиска введите **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-133">In the search box, type **Trakopolis**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="1dab2-135">На панели результатов выберите **Trakopolis** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="1dab2-135">In the results panel, select **Trakopolis**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dab2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dab2-138">В этом разделе описана настройка и проверка единого входа Azure AD в Trakopolis с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dab2-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dab2-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Trakopolis соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dab2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis is to a user in Azure AD.</span></span> <span data-ttu-id="1dab2-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-140">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>

<span data-ttu-id="1dab2-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-141">In Trakopolis, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1dab2-142">Чтобы настроить и проверить единый вход Azure AD в Trakopolis, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="1dab2-142">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1dab2-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="1dab2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1dab2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dab2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dab2-145">**[Создание тестового пользователя Trakopolis](#creating-a-trakopolis-test-user)** требуется для того, чтобы в Trakopolis существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dab2-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dab2-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dab2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dab2-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1dab2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dab2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dab2-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="1dab2-150">**Чтобы настроить единый вход Azure AD в Trakopolis, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1dab2-150">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="1dab2-151">На портале Azure на странице интеграции с приложением **Trakopolis** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-151">In the Azure portal, on the **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1dab2-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="1dab2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="1dab2-155">В разделе **Домены и URL-адреса приложения Trakopolis** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1dab2-155">On the **Trakopolis Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="1dab2-157">а.</span><span class="sxs-lookup"><span data-stu-id="1dab2-157">a.</span></span> <span data-ttu-id="1dab2-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="1dab2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="1dab2-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dab2-159">b.</span></span> <span data-ttu-id="1dab2-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="1dab2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1dab2-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1dab2-161">These values are not real.</span></span> <span data-ttu-id="1dab2-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="1dab2-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1dab2-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="1dab2-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) to get these values.</span></span> 

4. <span data-ttu-id="1dab2-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1dab2-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="1dab2-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1dab2-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1dab2-168">В разделе **Конфигурация Trakopolis** щелкните **Настроить Trakopolis**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-168">On the **Trakopolis Configuration** section, click **Configure Trakopolis** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1dab2-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="1dab2-171">Чтобы настроить единый вход на стороне **Trakopolis**, нужно отправить скачанный **XML-файл метаданных, URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="1dab2-171">To configure single sign-on on **Trakopolis** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="1dab2-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="1dab2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1dab2-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="1dab2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1dab2-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="1dab2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1dab2-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="1dab2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dab2-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dab2-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1dab2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1dab2-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="1dab2-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1dab2-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dab2-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dab2-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dab2-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1dab2-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dab2-188">а.</span><span class="sxs-lookup"><span data-stu-id="1dab2-188">a.</span></span> <span data-ttu-id="1dab2-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dab2-190">b.</span><span class="sxs-lookup"><span data-stu-id="1dab2-190">b.</span></span> <span data-ttu-id="1dab2-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1dab2-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dab2-192">c.</span><span class="sxs-lookup"><span data-stu-id="1dab2-192">c.</span></span> <span data-ttu-id="1dab2-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1dab2-194">d.</span><span class="sxs-lookup"><span data-stu-id="1dab2-194">d.</span></span> <span data-ttu-id="1dab2-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="1dab2-196">Создание тестового пользователя Trakopolis</span><span class="sxs-lookup"><span data-stu-id="1dab2-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="1dab2-197">В этом разделе описано, как создать пользователя Britta Simon в Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="1dab2-198">Обратитесь к [группе поддержки Trakopolis](mailto:support@cantelematics.com), чтобы добавить пользователей в учетную запись Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add the users in the Trakopolis platform.</span></span> <span data-ttu-id="1dab2-199">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="1dab2-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1dab2-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dab2-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1dab2-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakopolis.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1dab2-203">**Чтобы назначить пользователя Britta Simon в Trakopolis, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1dab2-203">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="1dab2-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1dab2-206">В списке приложений выберите **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-206">In the applications list, select **Trakopolis**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="1dab2-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1dab2-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-210">Click **Add** button.</span></span> <span data-ttu-id="1dab2-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1dab2-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1dab2-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dab2-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1dab2-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dab2-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1dab2-216">Testing single sign-on</span></span>

<span data-ttu-id="1dab2-217">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="1dab2-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="1dab2-218">Щелкнув элемент Trakopolis на панели доступа, вы автоматически войдете в приложение Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="1dab2-218">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dab2-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1dab2-219">Additional resources</span></span>

* [<span data-ttu-id="1dab2-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dab2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dab2-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1dab2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

