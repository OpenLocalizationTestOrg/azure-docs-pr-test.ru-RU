---
title: "Руководство по интеграции Azure Active Directory с Tidemark | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Tidemark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 170dc58363b12ec671c2fab8c80c7720d3dbf352
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="92dbc-103">Руководство. Интеграция Azure Active Directory с Tidemark</span><span class="sxs-lookup"><span data-stu-id="92dbc-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="92dbc-104">В этом руководстве описано, как интегрировать Tidemark с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92dbc-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92dbc-105">Интеграция Azure AD с приложением Tidemark обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="92dbc-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92dbc-106">С помощью Azure AD вы можете контролировать доступ к Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-106">You can control in Azure AD who has access to Tidemark</span></span>
- <span data-ttu-id="92dbc-107">Вы можете включить автоматический вход пользователей в Tidemark (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92dbc-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92dbc-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="92dbc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92dbc-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92dbc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92dbc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="92dbc-110">Prerequisites</span></span>

<span data-ttu-id="92dbc-111">Чтобы настроить интеграцию Azure AD с Tidemark, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="92dbc-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

- <span data-ttu-id="92dbc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="92dbc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92dbc-113">подписка Tidemark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="92dbc-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92dbc-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="92dbc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92dbc-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="92dbc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92dbc-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="92dbc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92dbc-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92dbc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92dbc-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="92dbc-118">Scenario description</span></span>
<span data-ttu-id="92dbc-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="92dbc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92dbc-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="92dbc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92dbc-121">Добавление Tidemark из коллекции</span><span class="sxs-lookup"><span data-stu-id="92dbc-121">Adding Tidemark from the gallery</span></span>
2. <span data-ttu-id="92dbc-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dbc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-the-gallery"></a><span data-ttu-id="92dbc-123">Добавление Tidemark из коллекции</span><span class="sxs-lookup"><span data-stu-id="92dbc-123">Adding Tidemark from the gallery</span></span>
<span data-ttu-id="92dbc-124">Чтобы настроить интеграцию Tidemark с Azure AD, необходимо добавить Tidemark из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="92dbc-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92dbc-125">**Чтобы добавить Tidemark из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="92dbc-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92dbc-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92dbc-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92dbc-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="92dbc-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="92dbc-133">В поле поиска введите **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-133">In the search box, type **Tidemark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="92dbc-135">На панели результатов выберите **Tidemark** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="92dbc-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92dbc-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dbc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92dbc-138">В этом разделе описана настройка и проверка единого входа Azure AD в Tidemark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92dbc-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92dbc-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Tidemark соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92dbc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span></span> <span data-ttu-id="92dbc-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="92dbc-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92dbc-142">Чтобы настроить и проверить единый вход Azure AD в Tidemark, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="92dbc-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92dbc-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="92dbc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92dbc-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92dbc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92dbc-145">**[Создание тестового пользователя Tidemark](#creating-a-tidemark-test-user)** требуется для того, чтобы в Tidemark существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92dbc-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92dbc-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92dbc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92dbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="92dbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92dbc-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dbc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92dbc-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="92dbc-150">**Чтобы настроить единый вход Azure AD в Tidemark, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="92dbc-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="92dbc-151">На портале Azure на странице интеграции с приложением **Tidemark** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="92dbc-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="92dbc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="92dbc-155">В разделе **Домены и URL-адреса приложения Tidemark** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="92dbc-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="92dbc-157">а.</span><span class="sxs-lookup"><span data-stu-id="92dbc-157">a.</span></span> <span data-ttu-id="92dbc-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="92dbc-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="92dbc-159">b.</span><span class="sxs-lookup"><span data-stu-id="92dbc-159">b.</span></span> <span data-ttu-id="92dbc-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="92dbc-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="92dbc-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="92dbc-161">These values are not real.</span></span> <span data-ttu-id="92dbc-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="92dbc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92dbc-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Tidemark](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="92dbc-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="92dbc-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="92dbc-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="92dbc-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="92dbc-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92dbc-168">В разделе **Конфигурация Tidemark** щелкните **Настроить Tidemark**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92dbc-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="92dbc-171">Чтобы настроить единый вход на стороне **Tidemark**, необходимо отправить скачанный **сертификат в кодировке Base64, идентификатор сущности SAML, URL-адрес выхода и URL-адрес службы единого входа SAML** [группе поддержки Tidemark](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="92dbc-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="92dbc-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="92dbc-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="92dbc-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="92dbc-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92dbc-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="92dbc-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92dbc-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="92dbc-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92dbc-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dbc-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="92dbc-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92dbc-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="92dbc-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="92dbc-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92dbc-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92dbc-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92dbc-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92dbc-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="92dbc-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92dbc-188">а.</span><span class="sxs-lookup"><span data-stu-id="92dbc-188">a.</span></span> <span data-ttu-id="92dbc-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92dbc-190">b.</span><span class="sxs-lookup"><span data-stu-id="92dbc-190">b.</span></span> <span data-ttu-id="92dbc-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92dbc-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92dbc-192">c.</span><span class="sxs-lookup"><span data-stu-id="92dbc-192">c.</span></span> <span data-ttu-id="92dbc-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92dbc-194">d.</span><span class="sxs-lookup"><span data-stu-id="92dbc-194">d.</span></span> <span data-ttu-id="92dbc-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="92dbc-196">Создание тестового пользователя Tidemark</span><span class="sxs-lookup"><span data-stu-id="92dbc-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="92dbc-197">Цель этого раздела — создать пользователя с именем Britta Simon в Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="92dbc-198">Обратитесь к [группе поддержки Tidemark](http://www.tidemark.com/contact-us), чтобы добавить пользователей в учетную запись Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92dbc-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="92dbc-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92dbc-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="92dbc-202">**Чтобы назначить пользователя Britta Simon в Tidemark, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="92dbc-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="92dbc-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="92dbc-205">В списке приложений выберите **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-205">In the applications list, select **Tidemark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="92dbc-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="92dbc-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-209">Click **Add** button.</span></span> <span data-ttu-id="92dbc-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="92dbc-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92dbc-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92dbc-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="92dbc-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92dbc-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="92dbc-215">Testing single sign-on</span></span>

<span data-ttu-id="92dbc-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="92dbc-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92dbc-217">Щелкнув элемент Tidemark на панели доступа, вы автоматически войдете в приложение Tidemark.</span><span class="sxs-lookup"><span data-stu-id="92dbc-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>
<span data-ttu-id="92dbc-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92dbc-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92dbc-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="92dbc-219">Additional resources</span></span>

* [<span data-ttu-id="92dbc-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92dbc-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92dbc-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92dbc-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

