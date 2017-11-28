---
title: "Руководство по интеграции Azure Active Directory с NetDocuments | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="b1a52-103">Учебник. Интеграция Azure Active Directory с NetDocuments</span><span class="sxs-lookup"><span data-stu-id="b1a52-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="b1a52-104">В этом руководстве описано, как интегрировать приложение NetDocuments с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1a52-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1a52-105">Интеграция Azure AD с приложением NetDocuments обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b1a52-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1a52-106">С помощью Azure AD вы можете контролировать доступ к NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="b1a52-107">Вы можете включить автоматический вход пользователей в NetDocuments (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1a52-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1a52-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a52-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b1a52-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1a52-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1a52-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1a52-110">Prerequisites</span></span>

<span data-ttu-id="b1a52-111">Чтобы настроить интеграцию Azure AD с NetDocuments, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b1a52-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="b1a52-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b1a52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1a52-113">подписка NetDocuments с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b1a52-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1a52-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b1a52-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1a52-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b1a52-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1a52-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b1a52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1a52-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1a52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1a52-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b1a52-118">Scenario description</span></span>
<span data-ttu-id="b1a52-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b1a52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1a52-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b1a52-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1a52-121">Добавление NetDocuments из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b1a52-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="b1a52-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1a52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="b1a52-123">Добавление NetDocuments из коллекции</span><span class="sxs-lookup"><span data-stu-id="b1a52-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="b1a52-124">Чтобы настроить интеграцию NetDocuments с Azure AD, необходимо добавить NetDocuments из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b1a52-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1a52-125">**Чтобы добавить NetDocuments из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b1a52-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1a52-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1a52-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1a52-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b1a52-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b1a52-133">В поле поиска введите **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-133">In the search box, type **NetDocuments**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="b1a52-135">На панели результатов выберите **NetDocuments** и щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b1a52-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1a52-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1a52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1a52-138">В этом разделе описаны настройка и проверка единого входа Azure AD в NetDocuments с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1a52-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1a52-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в NetDocuments соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1a52-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="b1a52-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="b1a52-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b1a52-142">Чтобы настроить и проверить единый вход Azure AD в NetDocuments, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b1a52-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1a52-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b1a52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1a52-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1a52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1a52-145">**[Создание тестового пользователя NetDocuments](#creating-a-netdocuments-test-user)** требуется для создания пользователя Britta Simon в NetDocuments, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1a52-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1a52-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1a52-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1a52-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b1a52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1a52-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1a52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1a52-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="b1a52-150">**Чтобы настроить единый вход Azure AD в NetDocuments, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b1a52-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="b1a52-151">На портале Azure на странице интеграции с приложением **NetDocuments** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b1a52-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b1a52-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="b1a52-155">В разделе **Домены и URL-адреса приложения NetDocuments** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b1a52-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="b1a52-157">а.</span><span class="sxs-lookup"><span data-stu-id="b1a52-157">a.</span></span> <span data-ttu-id="b1a52-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="b1a52-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="b1a52-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1a52-159">b.</span></span> <span data-ttu-id="b1a52-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`.</span><span class="sxs-lookup"><span data-stu-id="b1a52-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1a52-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b1a52-161">These values are not real.</span></span> <span data-ttu-id="b1a52-162">Измените их на фактические значения URL-адреса входа и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="b1a52-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="b1a52-163">Обратитесь к [службе поддержки NetDocuments](https://support.netdocuments.com/hc/), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="b1a52-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="b1a52-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b1a52-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="b1a52-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b1a52-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1a52-168">В другом окне веб-браузера войдите на сайт NetDocuments вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b1a52-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="b1a52-169">Откройте страницу **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="b1a52-170">Щелкните **Добавление и удаление пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="b1a52-171">![Репозиторий](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Репозиторий")</span><span class="sxs-lookup"><span data-stu-id="b1a52-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="b1a52-172">Щелкните **Настройка дополнительных параметров аутентификации**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="b1a52-173">![Настройка дополнительных параметров аутентификации](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Настройка дополнительных параметров аутентификации")</span><span class="sxs-lookup"><span data-stu-id="b1a52-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="b1a52-174">В диалоговом окне **Federated Identity** (Федеративное удостоверение) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b1a52-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b1a52-175">![Федеративное удостоверение](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Федеративное удостоверение")</span><span class="sxs-lookup"><span data-stu-id="b1a52-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="b1a52-176">а.</span><span class="sxs-lookup"><span data-stu-id="b1a52-176">a.</span></span> <span data-ttu-id="b1a52-177">Для параметра **Federated identity server type** (Тип сервера федеративных удостоверений) выберите **Службы федерации Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="b1a52-178">b.</span><span class="sxs-lookup"><span data-stu-id="b1a52-178">b.</span></span> <span data-ttu-id="b1a52-179">Щелкните **Выбрать файл**, чтобы отправить скачанный файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a52-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="b1a52-180">c.</span><span class="sxs-lookup"><span data-stu-id="b1a52-180">c.</span></span> <span data-ttu-id="b1a52-181">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="b1a52-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b1a52-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b1a52-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b1a52-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b1a52-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b1a52-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1a52-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1a52-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1a52-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1a52-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b1a52-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b1a52-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1a52-189">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1a52-191">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1a52-193">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1a52-195">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b1a52-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1a52-197">а.</span><span class="sxs-lookup"><span data-stu-id="b1a52-197">a.</span></span> <span data-ttu-id="b1a52-198">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1a52-199">b.</span><span class="sxs-lookup"><span data-stu-id="b1a52-199">b.</span></span> <span data-ttu-id="b1a52-200">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1a52-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1a52-201">c.</span><span class="sxs-lookup"><span data-stu-id="b1a52-201">c.</span></span> <span data-ttu-id="b1a52-202">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b1a52-203">d.</span><span class="sxs-lookup"><span data-stu-id="b1a52-203">d.</span></span> <span data-ttu-id="b1a52-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="b1a52-205">Создание тестового пользователя NetDocuments</span><span class="sxs-lookup"><span data-stu-id="b1a52-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="b1a52-206">Чтобы разрешить пользователям Azure AD вход в NetDocuments, их необходимо подготовить для NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="b1a52-207">В случае с NetDocuments подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b1a52-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="b1a52-208">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b1a52-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b1a52-209">Войдите на сайт компании **NetDocuments** от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b1a52-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="b1a52-210">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="b1a52-211">![Администратор](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="b1a52-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="b1a52-212">Щелкните **Добавление и удаление пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="b1a52-213">![Репозиторий](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Репозиторий")</span><span class="sxs-lookup"><span data-stu-id="b1a52-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="b1a52-214">В текстовом поле **Электронная почта** введите адрес электронной почты действующей учетной записи Azure Active Directory, которую вы хотите подготовить, а затем нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="b1a52-215">![Адрес электронной почты](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Адрес электронной почты")</span><span class="sxs-lookup"><span data-stu-id="b1a52-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="b1a52-216">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="b1a52-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="b1a52-217">Вы можете использовать любые другие инструменты создания учетных записей пользователя NetDocuments или API, предоставляемые NetDocuments для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b1a52-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b1a52-218">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1a52-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b1a52-219">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b1a52-221">**Чтобы назначить пользователя Britta Simon приложению NetDocuments, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b1a52-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="b1a52-222">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b1a52-224">В списке приложений выберите **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-224">In the applications list, select **NetDocuments**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="b1a52-226">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b1a52-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-228">Click **Add** button.</span></span> <span data-ttu-id="b1a52-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b1a52-231">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1a52-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1a52-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b1a52-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1a52-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b1a52-234">Testing single sign-on</span></span>

<span data-ttu-id="b1a52-235">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b1a52-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b1a52-236">Щелкнув элемент NetDocuments на панели доступа, вы автоматически войдете в приложение NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b1a52-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="b1a52-237">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1a52-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1a52-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b1a52-238">Additional resources</span></span>

* [<span data-ttu-id="b1a52-239">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1a52-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1a52-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1a52-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

