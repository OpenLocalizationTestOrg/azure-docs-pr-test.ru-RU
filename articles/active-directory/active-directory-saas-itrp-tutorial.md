---
title: "Руководство по интеграции Azure Active Directory с ITRP | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="7de82-103">Руководство по интеграции Azure Active Directory с ITRP</span><span class="sxs-lookup"><span data-stu-id="7de82-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="7de82-104">В этом руководстве описано, как интегрировать ITRP с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7de82-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7de82-105">Интеграция Azure AD с приложением ITRP обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7de82-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7de82-106">С помощью Azure AD вы можете контролировать доступ к ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="7de82-107">Вы можете включить автоматический вход для пользователей в ITRP (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de82-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7de82-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7de82-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7de82-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7de82-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7de82-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7de82-110">Prerequisites</span></span>

<span data-ttu-id="7de82-111">Чтобы настроить интеграцию Azure AD с ITRP, вам нужно:</span><span class="sxs-lookup"><span data-stu-id="7de82-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="7de82-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7de82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7de82-113">подписка ITRP с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7de82-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7de82-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7de82-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7de82-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7de82-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7de82-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7de82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7de82-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7de82-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7de82-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7de82-118">Scenario description</span></span>
<span data-ttu-id="7de82-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7de82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7de82-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7de82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7de82-121">Добавление ITRP из коллекции.</span><span class="sxs-lookup"><span data-stu-id="7de82-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="7de82-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="7de82-123">Добавление ITRP из коллекции</span><span class="sxs-lookup"><span data-stu-id="7de82-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="7de82-124">Чтобы настроить интеграцию ITRP с Azure AD, необходимо добавить ITRP из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7de82-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7de82-125">**Чтобы добавить ITRP из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7de82-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7de82-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7de82-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7de82-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de82-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7de82-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de82-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7de82-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7de82-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7de82-133">В поле поиска введите **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="7de82-133">In the search box, type **ITRP**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="7de82-135">На панели результатов выберите **ITRP** и выберите **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="7de82-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7de82-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de82-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="7de82-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ITRP с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de82-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7de82-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в ITRP соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de82-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="7de82-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="7de82-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7de82-142">Чтобы настроить и проверить единый вход Azure AD в ITRP, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="7de82-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7de82-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7de82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7de82-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7de82-145">**[Создание тестового пользователя ITRP](#creating-an-itrp-test-user)** требуется для создания в ITRP пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de82-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7de82-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7de82-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7de82-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7de82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7de82-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7de82-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="7de82-150">**Чтобы настроить единый вход Azure AD в ITRP, выполните следующее:**</span><span class="sxs-lookup"><span data-stu-id="7de82-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="7de82-151">На портале Azure на странице интеграции с приложением **ITRP** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7de82-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7de82-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7de82-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="7de82-155">В разделе **Домены и URL-адреса приложения ITRP** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7de82-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="7de82-157">а.</span><span class="sxs-lookup"><span data-stu-id="7de82-157">a.</span></span> <span data-ttu-id="7de82-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="7de82-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="7de82-159">b.</span><span class="sxs-lookup"><span data-stu-id="7de82-159">b.</span></span> <span data-ttu-id="7de82-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="7de82-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7de82-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7de82-161">These values are not real.</span></span> <span data-ttu-id="7de82-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="7de82-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7de82-163">Чтобы получить их, обратитесь в [службу поддержки клиентов ITRP](https://www.itrp.com/support).</span><span class="sxs-lookup"><span data-stu-id="7de82-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="7de82-164">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="7de82-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="7de82-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7de82-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7de82-168">В разделе **Настройка ITRP** выберите **Настроить ITRP**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7de82-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7de82-169">Скопируйте **URL-адрес службы единого входа SAML и URL-адрес выхода** из раздела **Краткий справочник**</span><span class="sxs-lookup"><span data-stu-id="7de82-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="7de82-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ITRP в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="7de82-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="7de82-172">На панели инструментов в верхней части экрана нажмите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="7de82-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="7de82-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="7de82-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="7de82-174">В левой области навигации нажмите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7de82-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="7de82-175">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775571.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7de82-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="7de82-176">В разделе конфигурации единого входа выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7de82-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="7de82-177">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775572.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7de82-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="7de82-178">![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775573.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7de82-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="7de82-179">а.</span><span class="sxs-lookup"><span data-stu-id="7de82-179">a.</span></span> <span data-ttu-id="7de82-180">Нажмите **Включить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-180">Click **Enable**.</span></span>

    <span data-ttu-id="7de82-181">b.</span><span class="sxs-lookup"><span data-stu-id="7de82-181">b.</span></span> <span data-ttu-id="7de82-182">В текстовое поле **URL-адрес удаленного выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7de82-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7de82-183">c.</span><span class="sxs-lookup"><span data-stu-id="7de82-183">c.</span></span> <span data-ttu-id="7de82-184">В текстовое поле **URL-адрес единого входа SAML** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7de82-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7de82-185">10.1. В текстовое поле **Certificate Fingerprint** (Отпечаток сертификата) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7de82-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="7de82-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7de82-187">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7de82-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7de82-188">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7de82-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7de82-189">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7de82-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7de82-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de82-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="7de82-191">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7de82-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7de82-193">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7de82-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7de82-194">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7de82-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7de82-196">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7de82-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7de82-198">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7de82-200">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7de82-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7de82-202">а.</span><span class="sxs-lookup"><span data-stu-id="7de82-202">a.</span></span> <span data-ttu-id="7de82-203">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7de82-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7de82-204">b.</span><span class="sxs-lookup"><span data-stu-id="7de82-204">b.</span></span> <span data-ttu-id="7de82-205">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7de82-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7de82-206">c.</span><span class="sxs-lookup"><span data-stu-id="7de82-206">c.</span></span> <span data-ttu-id="7de82-207">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7de82-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7de82-208">d.</span><span class="sxs-lookup"><span data-stu-id="7de82-208">d.</span></span> <span data-ttu-id="7de82-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7de82-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="7de82-210">Создание тестового пользователя ITRP</span><span class="sxs-lookup"><span data-stu-id="7de82-210">Creating an ITRP test user</span></span>

<span data-ttu-id="7de82-211">Чтобы пользователи Azure AD могли выполнять вход в ITRP, они должны быть подготовлены для ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="7de82-212">В случае с ITRP подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="7de82-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="7de82-213">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="7de82-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7de82-214">Выполните вход в клиент **ITRP** .</span><span class="sxs-lookup"><span data-stu-id="7de82-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="7de82-215">На панели инструментов в верхней части экрана нажмите **Записи**.</span><span class="sxs-lookup"><span data-stu-id="7de82-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="7de82-216">![Администратор](./media/active-directory-saas-itrp-tutorial/ic775575.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="7de82-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="7de82-217">В контекстном меню выберите пункт **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7de82-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="7de82-218">![Люди](./media/active-directory-saas-itrp-tutorial/ic775587.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="7de82-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="7de82-219">Нажмите **Добавить пользователя** ("+").</span><span class="sxs-lookup"><span data-stu-id="7de82-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="7de82-220">![Администратор](./media/active-directory-saas-itrp-tutorial/ic775576.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="7de82-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="7de82-221">В диалоговом окне "Добавить пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7de82-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="7de82-222">![Пользователь](./media/active-directory-saas-itrp-tutorial/ic775577.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="7de82-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="7de82-223">а.</span><span class="sxs-lookup"><span data-stu-id="7de82-223">a.</span></span> <span data-ttu-id="7de82-224">Введите атрибуты **Name** (Имя) и **Email** (Адрес электронной почты) действующей учетной записи AAD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="7de82-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="7de82-225">b.</span><span class="sxs-lookup"><span data-stu-id="7de82-225">b.</span></span> <span data-ttu-id="7de82-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="7de82-227">Вы можете использовать любые другие средства создания учетной записи пользователя ITRP или API, предоставляемые ITRP для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="7de82-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7de82-228">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7de82-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7de82-229">В этом разделе описано, как предоставить пользователю Britta Simon доступ к ITRP, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="7de82-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7de82-231">**Чтобы назначить пользователя Britta Simon в ITRP, выполните следующее:**</span><span class="sxs-lookup"><span data-stu-id="7de82-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="7de82-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7de82-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7de82-234">В списке приложений выберите **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="7de82-234">In the applications list, select **ITRP**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="7de82-236">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7de82-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7de82-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-238">Click **Add** button.</span></span> <span data-ttu-id="7de82-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7de82-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7de82-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7de82-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7de82-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7de82-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7de82-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7de82-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7de82-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7de82-244">Testing single sign-on</span></span>

<span data-ttu-id="7de82-245">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7de82-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7de82-246">Щелкнув элемент ITRP на панели доступа, вы автоматически войдете в приложение ITRP.</span><span class="sxs-lookup"><span data-stu-id="7de82-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="7de82-247">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7de82-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7de82-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7de82-248">Additional resources</span></span>

* [<span data-ttu-id="7de82-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7de82-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7de82-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7de82-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

