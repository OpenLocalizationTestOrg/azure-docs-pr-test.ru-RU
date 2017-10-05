---
title: "Руководство по интеграции Azure Active Directory с Gigya | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="857b8-103">Руководство. Интеграция Azure Active Directory с Gigya</span><span class="sxs-lookup"><span data-stu-id="857b8-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="857b8-104">В этом руководстве описано, как интегрировать Gigya с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="857b8-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="857b8-105">Интеграция Azure AD с приложением Gigya обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="857b8-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="857b8-106">С помощью Azure AD можно управлять доступом к Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="857b8-107">Вы можете включить автоматический вход пользователей в Gigya (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="857b8-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="857b8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="857b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="857b8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="857b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="857b8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="857b8-110">Prerequisites</span></span>

<span data-ttu-id="857b8-111">Чтобы настроить интеграцию Azure AD с Gigya, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="857b8-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="857b8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="857b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="857b8-113">подписка Gigya с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="857b8-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="857b8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="857b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="857b8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="857b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="857b8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="857b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="857b8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="857b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="857b8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="857b8-118">Scenario description</span></span>
<span data-ttu-id="857b8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="857b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="857b8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="857b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="857b8-121">Добавление Gigya из коллекции</span><span class="sxs-lookup"><span data-stu-id="857b8-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="857b8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="857b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="857b8-123">Добавление Gigya из коллекции</span><span class="sxs-lookup"><span data-stu-id="857b8-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="857b8-124">Чтобы настроить интеграцию Gigya с Azure AD, необходимо добавить Gigya из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="857b8-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="857b8-125">**Чтобы добавить Gigya из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="857b8-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="857b8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="857b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="857b8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="857b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="857b8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="857b8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="857b8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="857b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="857b8-133">В поле поиска введите **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="857b8-133">In the search box, type **Gigya**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="857b8-135">На панели результатов выберите **Gigya** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="857b8-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="857b8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="857b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="857b8-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Gigya с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="857b8-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="857b8-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Gigya соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="857b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="857b8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="857b8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="857b8-142">Чтобы настроить и проверить единый вход Azure AD в Gigya, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="857b8-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="857b8-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="857b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="857b8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="857b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="857b8-145">**[Создание тестового пользователя Gigya](#creating-a-gigya-test-user)** требуется для создания в Gigya пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="857b8-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="857b8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="857b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="857b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="857b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="857b8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="857b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="857b8-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="857b8-150">**Чтобы настроить единый вход Azure AD в Gigya, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="857b8-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="857b8-151">На портале Azure на странице интеграции с приложением **Gigya** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="857b8-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="857b8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="857b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="857b8-155">В разделе **Домен и URL-адреса приложения Gigya** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="857b8-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="857b8-157">а.</span><span class="sxs-lookup"><span data-stu-id="857b8-157">a.</span></span> <span data-ttu-id="857b8-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="857b8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="857b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="857b8-159">b.</span></span> <span data-ttu-id="857b8-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="857b8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="857b8-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="857b8-161">These values are not real.</span></span> <span data-ttu-id="857b8-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="857b8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="857b8-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Gigya](https://www.gigya.com/support-policy/).</span><span class="sxs-lookup"><span data-stu-id="857b8-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="857b8-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="857b8-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="857b8-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="857b8-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="857b8-168">В разделе **Настройка Gigya** щелкните **Настроить Gigya**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="857b8-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="857b8-169">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="857b8-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="857b8-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Gigya в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="857b8-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="857b8-172">Последовательно выберите **Settings \> SAML Login** (Параметры > Вход SAML) и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="857b8-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="857b8-173">![Вход SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Вход SAML")</span><span class="sxs-lookup"><span data-stu-id="857b8-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="857b8-174">В разделе **Вход SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="857b8-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="857b8-175">![Настройка SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="857b8-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="857b8-176">а.</span><span class="sxs-lookup"><span data-stu-id="857b8-176">a.</span></span> <span data-ttu-id="857b8-177">В текстовом поле **Имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="857b8-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="857b8-178">b.</span><span class="sxs-lookup"><span data-stu-id="857b8-178">b.</span></span> <span data-ttu-id="857b8-179">В текстовое поле **Издатель** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="857b8-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="857b8-180">c.</span><span class="sxs-lookup"><span data-stu-id="857b8-180">c.</span></span> <span data-ttu-id="857b8-181">В текстовое поле **URL-адрес службы единого входа** вставьте значение **URL-адреса службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="857b8-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="857b8-182">г)</span><span class="sxs-lookup"><span data-stu-id="857b8-182">d.</span></span> <span data-ttu-id="857b8-183">В текстовое поле **Формат идентификатора имени** вставьте значение **формата идентификатора имени**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="857b8-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="857b8-184">д.</span><span class="sxs-lookup"><span data-stu-id="857b8-184">e.</span></span> <span data-ttu-id="857b8-185">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="857b8-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="857b8-186">Е.</span><span class="sxs-lookup"><span data-stu-id="857b8-186">f.</span></span> <span data-ttu-id="857b8-187">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="857b8-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="857b8-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="857b8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="857b8-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="857b8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="857b8-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="857b8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="857b8-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="857b8-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="857b8-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="857b8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="857b8-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="857b8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="857b8-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="857b8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="857b8-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="857b8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="857b8-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="857b8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="857b8-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="857b8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="857b8-203">а.</span><span class="sxs-lookup"><span data-stu-id="857b8-203">a.</span></span> <span data-ttu-id="857b8-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="857b8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="857b8-205">b.</span><span class="sxs-lookup"><span data-stu-id="857b8-205">b.</span></span> <span data-ttu-id="857b8-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="857b8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="857b8-207">c.</span><span class="sxs-lookup"><span data-stu-id="857b8-207">c.</span></span> <span data-ttu-id="857b8-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="857b8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="857b8-209">d.</span><span class="sxs-lookup"><span data-stu-id="857b8-209">d.</span></span> <span data-ttu-id="857b8-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="857b8-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="857b8-211">Создание тестового пользователя Gigya</span><span class="sxs-lookup"><span data-stu-id="857b8-211">Creating a Gigya test user</span></span>

<span data-ttu-id="857b8-212">Чтобы пользователи Azure AD могли выполнять вход в Gigya, они должны быть подготовлены для Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="857b8-213">В случае с Gigya подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="857b8-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="857b8-214">Чтобы подготовить учетные записи пользователей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="857b8-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="857b8-215">Выполните вход на корпоративный веб-сайт **Gigya** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="857b8-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="857b8-216">Последовательно выберите **Admin \> Manage Users** (Администратор > Управление пользователями) и нажмите кнопку **Invite Users** (Пригласить пользователей).</span><span class="sxs-lookup"><span data-stu-id="857b8-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="857b8-217">![Управление пользователями](./media/active-directory-saas-gigya-tutorial/ic789535.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="857b8-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="857b8-218">В диалоговом окне "Пригласить пользователей" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="857b8-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="857b8-219">![Приглашение пользователей](./media/active-directory-saas-gigya-tutorial/ic789536.png "приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="857b8-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="857b8-220">а.</span><span class="sxs-lookup"><span data-stu-id="857b8-220">a.</span></span> <span data-ttu-id="857b8-221">В текстовое поле **Электронная почта** введите адрес электронной почты действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="857b8-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="857b8-222">b.</span><span class="sxs-lookup"><span data-stu-id="857b8-222">b.</span></span> <span data-ttu-id="857b8-223">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="857b8-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="857b8-224">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="857b8-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="857b8-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="857b8-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="857b8-226">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="857b8-228">**Чтобы назначить пользователя Britta Simon в Gigya, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="857b8-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="857b8-229">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="857b8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="857b8-231">В списке приложений выберите **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="857b8-231">In the applications list, select **Gigya**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="857b8-233">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="857b8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="857b8-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="857b8-235">Click **Add** button.</span></span> <span data-ttu-id="857b8-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="857b8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="857b8-238">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="857b8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="857b8-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="857b8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="857b8-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="857b8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="857b8-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="857b8-241">Testing single sign-on</span></span>

<span data-ttu-id="857b8-242">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="857b8-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="857b8-243">Щелкнув плитку Gigya на панели доступа, вы автоматически войдете в приложение Gigya.</span><span class="sxs-lookup"><span data-stu-id="857b8-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="857b8-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="857b8-244">Additional resources</span></span>

* [<span data-ttu-id="857b8-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="857b8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="857b8-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="857b8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

