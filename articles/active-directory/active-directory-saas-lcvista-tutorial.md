---
title: "Руководство. Интеграция Azure Active Directory с LCVista | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="b2843-103">Руководство. Интеграция Azure Active Directory с LCVista</span><span class="sxs-lookup"><span data-stu-id="b2843-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="b2843-104">В этом руководстве описано, как интегрировать LCVista с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2843-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2843-105">Интеграция LCVista c Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b2843-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b2843-106">В Azure AD вы сможете контролировать, у кого есть доступ к LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="b2843-107">Вы можете включить автоматический вход пользователей в LCVista (единый вход) с помощью их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2843-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2843-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b2843-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b2843-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2843-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2843-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b2843-110">Prerequisites</span></span>

<span data-ttu-id="b2843-111">Чтобы настроить интеграцию Azure AD с LCVista, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="b2843-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="b2843-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b2843-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2843-113">подписка LCVista с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b2843-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2843-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b2843-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2843-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b2843-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2843-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b2843-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2843-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2843-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2843-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b2843-118">Scenario description</span></span>
<span data-ttu-id="b2843-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b2843-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2843-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="b2843-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2843-121">Добавления LCVista из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b2843-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="b2843-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2843-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="b2843-123">Добавления LCVista из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b2843-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="b2843-124">Чтобы настроить интеграцию LCVista в Azure AD, необходимо добавить LCVista из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b2843-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b2843-125">**Чтобы добавить LCVista из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b2843-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b2843-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b2843-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b2843-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b2843-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b2843-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b2843-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b2843-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b2843-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b2843-133">В поле поиска введите **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="b2843-133">In the search box, type **LCVista**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="b2843-135">На панели результатов выберите **LCVista**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b2843-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2843-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2843-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2843-138">В этом разделе описана настройка и проверка единого входа Azure AD в LCVista с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2843-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b2843-139">Чтобы настроить единый вход Azure AD, Azure AD необходимо знать, какой пользователь в LCVista соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2843-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="b2843-140">Другими словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="b2843-141">Чтобы установить эту связь, следует назначить значение **имени пользователя** в Azure AD в качестве значения **имени пользователя** в LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="b2843-142">Чтобы настроить и проверить единый вход Azure AD в LCVista, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b2843-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b2843-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b2843-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b2843-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2843-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b2843-145">**[Создание тестового пользователя LCVista](#creating-a-lcvista-test-user)** требуется для создания в LCVista пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2843-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b2843-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2843-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2843-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b2843-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2843-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2843-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2843-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure, а также как настроить его в приложении LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="b2843-150">**Чтобы настроить единый вход Azure AD в LCVista, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b2843-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="b2843-151">На портале Azure на странице интеграции с приложением **LCVista** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b2843-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b2843-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b2843-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="b2843-155">В разделе **Домены и URL-адреса приложения LCVista** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b2843-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="b2843-157">а.</span><span class="sxs-lookup"><span data-stu-id="b2843-157">a.</span></span> <span data-ttu-id="b2843-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="b2843-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="b2843-159">b.</span><span class="sxs-lookup"><span data-stu-id="b2843-159">b.</span></span> <span data-ttu-id="b2843-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="b2843-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="b2843-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b2843-161">These values are not the real.</span></span> <span data-ttu-id="b2843-162">Измените их на фактические значения идентификатора и URL-адреса единого входа.</span><span class="sxs-lookup"><span data-stu-id="b2843-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="b2843-163">Чтобы получить их, обратитесь в [службу поддержки клиентов LCVista](https://lcvista.com/contact).</span><span class="sxs-lookup"><span data-stu-id="b2843-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="b2843-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b2843-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="b2843-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b2843-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b2843-168">В разделе **Конфигурация LCVista** щелкните **настройку LCVista**, чтобы открыть окно **настройки единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b2843-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b2843-169">Скопируйте **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b2843-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="b2843-171">Войдите в приложение LCVista как администратор.</span><span class="sxs-lookup"><span data-stu-id="b2843-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="b2843-172">В разделе **SAML Config** (Конфигурация SAML) установите флажок **Enable SAML login** (Включить вход SAML), а затем введите сведения, представленные на изображении ниже.</span><span class="sxs-lookup"><span data-stu-id="b2843-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="b2843-174">а.</span><span class="sxs-lookup"><span data-stu-id="b2843-174">a.</span></span> <span data-ttu-id="b2843-175">Вставьте **URL-адрес издателя**, скопированный из Azure AD в раздел **Идентификатор сущности**.</span><span class="sxs-lookup"><span data-stu-id="b2843-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="b2843-176">b.</span><span class="sxs-lookup"><span data-stu-id="b2843-176">b.</span></span> <span data-ttu-id="b2843-177">Вставьте **URL-адрес службы единого входа**, скопированный из Azure AD в раздел **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="b2843-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="b2843-178">c.</span><span class="sxs-lookup"><span data-stu-id="b2843-178">c.</span></span> <span data-ttu-id="b2843-179">Из метаданных (XML), которые вы скачали на портале Azure, скопируйте значение **X509Certificate** и вставьте его в раздел **x509 Certificate** (Сертификат x509).</span><span class="sxs-lookup"><span data-stu-id="b2843-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="b2843-180">г)</span><span class="sxs-lookup"><span data-stu-id="b2843-180">d.</span></span> <span data-ttu-id="b2843-181">В текстовом поле **First name attribute** (Атрибут имени) вставьте значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="b2843-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="b2843-182">д.</span><span class="sxs-lookup"><span data-stu-id="b2843-182">e.</span></span> <span data-ttu-id="b2843-183">В текстовом поле **Last name attribute** (Атрибут фамилии) вставьте значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="b2843-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="b2843-184">f.</span><span class="sxs-lookup"><span data-stu-id="b2843-184">f.</span></span> <span data-ttu-id="b2843-185">В текстовом поле **Email attribute** (Атрибут электронной почты) вставьте значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="b2843-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="b2843-186">g.</span><span class="sxs-lookup"><span data-stu-id="b2843-186">g.</span></span> <span data-ttu-id="b2843-187">В текстовом поле **Username** (Атрибут имени пользователя) вставьте значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="b2843-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="b2843-188">д.</span><span class="sxs-lookup"><span data-stu-id="b2843-188">e.</span></span> <span data-ttu-id="b2843-189">Нажмите кнопку **Сохранить** , чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="b2843-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="b2843-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b2843-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b2843-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b2843-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b2843-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b2843-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2843-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2843-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2843-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2843-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b2843-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b2843-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b2843-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b2843-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2843-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b2843-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2843-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b2843-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2843-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b2843-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2843-205">а.</span><span class="sxs-lookup"><span data-stu-id="b2843-205">a.</span></span> <span data-ttu-id="b2843-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2843-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2843-207">b.</span><span class="sxs-lookup"><span data-stu-id="b2843-207">b.</span></span> <span data-ttu-id="b2843-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b2843-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2843-209">c.</span><span class="sxs-lookup"><span data-stu-id="b2843-209">c.</span></span> <span data-ttu-id="b2843-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b2843-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b2843-211">d.</span><span class="sxs-lookup"><span data-stu-id="b2843-211">d.</span></span> <span data-ttu-id="b2843-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b2843-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="b2843-213">Создание тестового пользователя LCVista</span><span class="sxs-lookup"><span data-stu-id="b2843-213">Creating a LCVista test user</span></span>

<span data-ttu-id="b2843-214">В этом разделе описано, как создать пользователя Britta Simon в LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="b2843-215">Вам следует обратиться в [службу поддержки клиентов LCVista](https://lcvista.com/contact), чтобы добавить пользователей в приложение LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b2843-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2843-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b2843-217">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure с помощью предоставления доступа к LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b2843-219">**Чтобы назначить пользователя Britta Simon в LCVista, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b2843-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="b2843-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b2843-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b2843-222">В списке приложений выберите **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="b2843-222">In the applications list, select **LCVista**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="b2843-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b2843-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b2843-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b2843-226">Click **Add** button.</span></span> <span data-ttu-id="b2843-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b2843-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b2843-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b2843-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b2843-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b2843-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2843-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b2843-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2843-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b2843-232">Testing single sign-on</span></span>

<span data-ttu-id="b2843-233">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b2843-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="b2843-234">Щелкните плитку LCVista на панели доступа. Вы будете перенаправлены на страницу входа организации.</span><span class="sxs-lookup"><span data-stu-id="b2843-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="b2843-235">После успешного входа вы сможете войти в приложение LCVista.</span><span class="sxs-lookup"><span data-stu-id="b2843-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="b2843-236">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b2843-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b2843-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b2843-237">Additional resources</span></span>

* [<span data-ttu-id="b2843-238">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2843-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2843-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b2843-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

