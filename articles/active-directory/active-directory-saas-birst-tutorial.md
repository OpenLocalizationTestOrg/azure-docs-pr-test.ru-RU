---
title: "Руководство по интеграции Azure Active Directory с Birst Agile Business Analytics | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Birst Agile Business Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="4b63d-103">Руководство. Интеграция Azure Active Directory с Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="4b63d-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="4b63d-104">В этом руководстве описано, как интегрировать Birst Agile Business Analytics с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b63d-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b63d-105">Интеграция Azure AD с приложением Birst Agile Business Analytics обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4b63d-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b63d-106">С помощью Azure AD вы можете контролировать доступ к Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="4b63d-107">Вы можете включить автоматический вход пользователей в Birst Agile Business Analytics (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b63d-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b63d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4b63d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b63d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b63d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b63d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4b63d-110">Prerequisites</span></span>

<span data-ttu-id="4b63d-111">Чтобы настроить интеграцию Azure AD с Birst Agile Business Analytics, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="4b63d-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="4b63d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4b63d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b63d-113">подписка на Birst Agile Business Analytics с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4b63d-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b63d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="4b63d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b63d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="4b63d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b63d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4b63d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b63d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b63d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b63d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4b63d-118">Scenario description</span></span>
<span data-ttu-id="4b63d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4b63d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b63d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="4b63d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b63d-121">Добавление Birst Agile Business Analytics из коллекции</span><span class="sxs-lookup"><span data-stu-id="4b63d-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="4b63d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="4b63d-123">Добавление Birst Agile Business Analytics из коллекции</span><span class="sxs-lookup"><span data-stu-id="4b63d-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="4b63d-124">Чтобы настроить интеграцию Birst Agile Business Analytics с Azure AD, необходимо добавить Birst Agile Business Analytics из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b63d-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b63d-125">**Чтобы добавить Birst Agile Business Analytics из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="4b63d-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b63d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b63d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b63d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4b63d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4b63d-133">В поле поиска введите **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="4b63d-135">В области результатов выберите **Birst Agile Business Analytics** и нажмите кнопку **Добавить**, чтобы добавить эту программу.</span><span class="sxs-lookup"><span data-stu-id="4b63d-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b63d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b63d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Birst Agile Business Analytics с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b63d-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b63d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Birst Agile Business Analytics соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b63d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="4b63d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="4b63d-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b63d-142">Чтобы настроить и проверить единый вход Azure AD в Birst Agile Business Analytics, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="4b63d-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b63d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="4b63d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b63d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b63d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b63d-145">**[Создание тестового пользователя Birst Agile Business Analytics](#creating-a-birst-agile-business-analytics-test-user)** нужно для того, чтобы в Birst Agile Business Analytics также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b63d-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b63d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b63d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b63d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4b63d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b63d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b63d-149">В этом разделе описано, как включить единый вход Azure AD на новом Azure и настроить его в приложении Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="4b63d-150">**Чтобы настроить единый вход Azure AD в Birst Agile Business Analytics, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="4b63d-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="4b63d-151">На портале Azure на странице интеграции с приложением **Birst Agile Business Analytics** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4b63d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="4b63d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="4b63d-155">В разделе **Домены и URL-адреса приложения Birst Agile Business Analytics** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="4b63d-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="4b63d-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="4b63d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="4b63d-158">URL-адрес зависит от центра обработки данных, в котором расположена учетная запись Birst.</span><span class="sxs-lookup"><span data-stu-id="4b63d-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="4b63d-159">Для центра обработки данных в США используйте шаблон `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`.</span><span class="sxs-lookup"><span data-stu-id="4b63d-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="4b63d-160">Для центра обработки данных в Европе используйте шаблон `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`.</span><span class="sxs-lookup"><span data-stu-id="4b63d-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b63d-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="4b63d-161">This value is not real.</span></span> <span data-ttu-id="4b63d-162">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4b63d-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="4b63d-163">Обратитесь к [группе поддержки Birst Agile Business Analytics](mailto:info@birst.com) для получения этого значения.</span><span class="sxs-lookup"><span data-stu-id="4b63d-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="4b63d-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="4b63d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="4b63d-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4b63d-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b63d-168">В разделе **Конфигурация Birst Agile Business Analytics** щелкните **Настроить Birst Agile Business Analytics**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b63d-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="4b63d-171">Чтобы настроить единый вход на стороне **Birst Agile Business Analytics**, нужно отправить скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="4b63d-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="4b63d-172">Укажите в письме к группе поддержки Birst, что для интеграции необходимо использовать алгоритм SHA256 (SHA1 не будет поддерживаться), чтобы специалисты по поддержке настроили единый вход на соответствующем сервере, например **app2101**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="4b63d-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="4b63d-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b63d-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="4b63d-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b63d-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4b63d-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b63d-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63d-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b63d-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b63d-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4b63d-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4b63d-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b63d-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b63d-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b63d-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b63d-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4b63d-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b63d-188">а.</span><span class="sxs-lookup"><span data-stu-id="4b63d-188">a.</span></span> <span data-ttu-id="4b63d-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b63d-190">b.</span><span class="sxs-lookup"><span data-stu-id="4b63d-190">b.</span></span> <span data-ttu-id="4b63d-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b63d-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b63d-192">c.</span><span class="sxs-lookup"><span data-stu-id="4b63d-192">c.</span></span> <span data-ttu-id="4b63d-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b63d-194">d.</span><span class="sxs-lookup"><span data-stu-id="4b63d-194">d.</span></span> <span data-ttu-id="4b63d-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="4b63d-196">Создание тестового пользователя Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="4b63d-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="4b63d-197">В этом разделе описано, как создать пользователя с именем Britta Simon в Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="4b63d-198">Для добавления пользователей в учетную запись Birst следует обратиться к [группе поддержки Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="4b63d-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b63d-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b63d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b63d-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4b63d-202">**Чтобы назначить пользователя Britta Simon в Birst Agile Business Analytics, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="4b63d-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="4b63d-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4b63d-205">В списке приложений выберите **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="4b63d-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4b63d-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-209">Click **Add** button.</span></span> <span data-ttu-id="4b63d-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4b63d-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b63d-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b63d-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4b63d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b63d-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4b63d-215">Testing single sign-on</span></span>

<span data-ttu-id="4b63d-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4b63d-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4b63d-217">Щелкнув элемент Birst Agile Business Analytics на панели доступа, вы автоматически войдете в приложение Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="4b63d-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4b63d-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4b63d-218">Additional resources</span></span>

* [<span data-ttu-id="4b63d-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b63d-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b63d-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b63d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

