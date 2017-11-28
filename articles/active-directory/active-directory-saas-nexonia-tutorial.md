---
title: "Руководство по интеграции Azure Active Directory с Nexonia | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="40c93-103">Руководство по интеграции Azure Active Directory с Nexonia</span><span class="sxs-lookup"><span data-stu-id="40c93-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="40c93-104">В этом руководстве описано, как интегрировать Nexonia с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40c93-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40c93-105">Интеграция Azure AD с приложением Nexonia обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="40c93-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="40c93-106">С помощью Azure AD вы можете контролировать доступ к Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="40c93-107">Вы можете включить автоматический вход пользователей в Nexonia (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40c93-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40c93-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40c93-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="40c93-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="40c93-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="40c93-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40c93-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40c93-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="40c93-111">Prerequisites</span></span>

<span data-ttu-id="40c93-112">Чтобы настроить интеграцию Azure AD с Nexonia, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="40c93-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="40c93-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="40c93-113">An Azure AD subscription</span></span>
- <span data-ttu-id="40c93-114">подписка на Nexonia с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="40c93-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40c93-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="40c93-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40c93-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="40c93-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40c93-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="40c93-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40c93-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40c93-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40c93-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="40c93-119">Scenario description</span></span>
<span data-ttu-id="40c93-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="40c93-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40c93-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="40c93-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40c93-122">Добавление Nexonia из коллекции.</span><span class="sxs-lookup"><span data-stu-id="40c93-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="40c93-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40c93-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="40c93-124">Добавление Nexonia из коллекции</span><span class="sxs-lookup"><span data-stu-id="40c93-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="40c93-125">Чтобы настроить интеграцию Nexonia с Azure AD, необходимо добавить Nexonia из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="40c93-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="40c93-126">**Чтобы добавить Nexonia из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="40c93-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="40c93-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40c93-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40c93-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="40c93-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="40c93-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40c93-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="40c93-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="40c93-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="40c93-134">В поле поиска введите **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="40c93-134">In the search box, type **Nexonia**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="40c93-136">На панели результатов выберите **Nexonia** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="40c93-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40c93-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40c93-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40c93-139">В этом разделе описана настройка и проверка единого входа Azure AD в Nexonia с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40c93-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="40c93-140">Чтобы настроить единый вход Azure AD, необходимо знать, какой пользователь в Nexonia соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40c93-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="40c93-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="40c93-142">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="40c93-143">Чтобы настроить и проверить единый вход Azure AD в Nexonia, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="40c93-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="40c93-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="40c93-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="40c93-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40c93-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40c93-146">**[Создание тестового пользователя Nexonia](#creating-a-nexonia-test-user)** требуется для создания в Nexonia пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40c93-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="40c93-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40c93-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40c93-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40c93-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40c93-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40c93-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40c93-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="40c93-151">Если при интеграции возникают проблемы, воспользуйтесь этой [ссылкой](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) для ознакомления с руководством по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="40c93-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="40c93-152">Если вам по-прежнему не удается найти решение, направьте запрос в службу поддержки через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40c93-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="40c93-153">**Чтобы настроить единый вход Azure AD в Nexonia, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="40c93-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="40c93-154">На портале Azure на странице интеграции с приложением **Nexonia** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="40c93-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="40c93-156">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="40c93-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="40c93-158">В разделе **Домены и URL-адреса приложения Nexonia** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="40c93-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="40c93-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`.</span><span class="sxs-lookup"><span data-stu-id="40c93-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="40c93-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="40c93-161">This value is not real.</span></span> <span data-ttu-id="40c93-162">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="40c93-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="40c93-163">Чтобы получить это значение, обратитесь в [службу поддержки Nexonia](https://nexonia.zendesk.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="40c93-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="40c93-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="40c93-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="40c93-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="40c93-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40c93-168">В разделе **Конфигурация Nexonia** щелкните **Настроить Nexonia**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="40c93-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="40c93-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="40c93-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="40c93-171">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки Nexonia](https://nexonia.zendesk.com/hc/requests/new) и предоставьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="40c93-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="40c93-172">• скачанный **сертификат**</span><span class="sxs-lookup"><span data-stu-id="40c93-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="40c93-173">• **идентификатор сущности SAML**;</span><span class="sxs-lookup"><span data-stu-id="40c93-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="40c93-174">• **URL-адрес службы единого входа SAML**;</span><span class="sxs-lookup"><span data-stu-id="40c93-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="40c93-175">• **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="40c93-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="40c93-176">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="40c93-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="40c93-177">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="40c93-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="40c93-178">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="40c93-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40c93-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40c93-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="40c93-180">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40c93-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="40c93-182">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="40c93-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="40c93-183">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="40c93-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40c93-185">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="40c93-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40c93-187">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40c93-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40c93-189">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="40c93-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40c93-191">а.</span><span class="sxs-lookup"><span data-stu-id="40c93-191">a.</span></span> <span data-ttu-id="40c93-192">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40c93-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40c93-193">b.</span><span class="sxs-lookup"><span data-stu-id="40c93-193">b.</span></span> <span data-ttu-id="40c93-194">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40c93-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40c93-195">c.</span><span class="sxs-lookup"><span data-stu-id="40c93-195">c.</span></span> <span data-ttu-id="40c93-196">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="40c93-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="40c93-197">d.</span><span class="sxs-lookup"><span data-stu-id="40c93-197">d.</span></span> <span data-ttu-id="40c93-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40c93-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="40c93-199">Создание тестового пользователя Nexonia</span><span class="sxs-lookup"><span data-stu-id="40c93-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="40c93-200">В этом разделе описано, как создать пользователя Britta Simon в приложении Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="40c93-201">Обратитесь в [службу поддержки Nexonia](https://nexonia.zendesk.com/hc/requests/new), чтобы добавить пользователей на платформу Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="40c93-202">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="40c93-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="40c93-203">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40c93-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="40c93-204">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="40c93-206">**Чтобы назначить пользователя Britta Simon в Nexonia, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="40c93-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="40c93-207">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40c93-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="40c93-209">В списке приложений выберите **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="40c93-209">In the applications list, select **Nexonia**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="40c93-211">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40c93-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="40c93-213">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40c93-213">Click **Add** button.</span></span> <span data-ttu-id="40c93-214">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40c93-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="40c93-216">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="40c93-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="40c93-217">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="40c93-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40c93-218">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="40c93-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40c93-219">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="40c93-219">Testing single sign-on</span></span>

<span data-ttu-id="40c93-220">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="40c93-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="40c93-221">Щелкнув плитку Nexonia на панели доступа, вы автоматически войдете в приложение Nexonia.</span><span class="sxs-lookup"><span data-stu-id="40c93-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="40c93-222">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="40c93-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40c93-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40c93-223">Additional resources</span></span>

* [<span data-ttu-id="40c93-224">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40c93-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40c93-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40c93-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

