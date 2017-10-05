---
title: "Руководство по интеграции Azure Active Directory с Sprinklr | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="c04f1-103">Учебник. Интеграция Azure Active Directory с Sprinklr</span><span class="sxs-lookup"><span data-stu-id="c04f1-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="c04f1-104">В этом руководстве описано, как интегрировать Sprinklr с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c04f1-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c04f1-105">Интеграция Sprinklr с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c04f1-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c04f1-106">С помощью Azure AD вы можете контролировать доступ к Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="c04f1-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="c04f1-107">Вы можете включить автоматический вход пользователей в Sprinklr (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c04f1-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c04f1-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c04f1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c04f1-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c04f1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c04f1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c04f1-110">Prerequisites</span></span>

<span data-ttu-id="c04f1-111">Чтобы настроить интеграцию Azure AD с Sprinklr, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c04f1-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="c04f1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c04f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c04f1-113">подписка Sprinklr с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c04f1-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c04f1-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c04f1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c04f1-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c04f1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c04f1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c04f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c04f1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c04f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c04f1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c04f1-118">Scenario description</span></span>
<span data-ttu-id="c04f1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c04f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c04f1-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c04f1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c04f1-121">Добавление Sprinklr из коллекции</span><span class="sxs-lookup"><span data-stu-id="c04f1-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="c04f1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="c04f1-123">Добавление Sprinklr из коллекции</span><span class="sxs-lookup"><span data-stu-id="c04f1-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="c04f1-124">Чтобы настроить интеграцию Sprinklr с Azure AD, необходимо добавить Sprinklr из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c04f1-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c04f1-125">**Чтобы добавить Sprinklr из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c04f1-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c04f1-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c04f1-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c04f1-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c04f1-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c04f1-133">В поле поиска введите **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-133">In the search box, type **Sprinklr**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="c04f1-135">На панели результатов выберите **Sprinklr** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c04f1-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c04f1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c04f1-138">В этом разделе описана настройка и проверка единого входа Azure AD в Sprinklr для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c04f1-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c04f1-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Sprinklr соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c04f1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="c04f1-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="c04f1-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="c04f1-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="c04f1-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c04f1-142">Чтобы настроить и проверить единый вход в Azure AD в Sprinklr, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="c04f1-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c04f1-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c04f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c04f1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c04f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c04f1-145">**[Создание тестового пользователя Sprinklr](#creating-a-sprinklr-test-user)** требуется для создания пользователя Britta Simon в Sprinklr, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c04f1-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c04f1-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c04f1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c04f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c04f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c04f1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c04f1-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="c04f1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="c04f1-150">**Чтобы настроить единый вход Azure AD в Sprinklr, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c04f1-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="c04f1-151">На портале Azure на странице интеграции с приложением **Sprinklr** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c04f1-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c04f1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="c04f1-155">В разделе **Домены и URL-адреса Sprinklr** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c04f1-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="c04f1-157">а.</span><span class="sxs-lookup"><span data-stu-id="c04f1-157">a.</span></span> <span data-ttu-id="c04f1-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="c04f1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="c04f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="c04f1-159">b.</span></span> <span data-ttu-id="c04f1-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="c04f1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c04f1-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c04f1-161">These values are not real.</span></span> <span data-ttu-id="c04f1-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c04f1-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c04f1-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Sprinklr](https://www.sprinklr.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="c04f1-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="c04f1-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c04f1-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="c04f1-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c04f1-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c04f1-168">В разделе **Настройка Sprinklr** щелкните **Настроить Sprinklr**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c04f1-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="c04f1-170">В другом окне веб-браузера войдите на сайт Sprinklr своей организации в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c04f1-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="c04f1-171">Выберите **Administration (Администрирование) \> Settings (Параметры)**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="c04f1-172">![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="c04f1-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="c04f1-173">В области слева выберите **Manage Partner (Управление партнером) \> Single Sign (Единый вход)**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="c04f1-174">![Управление партнером](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Управление партнером")</span><span class="sxs-lookup"><span data-stu-id="c04f1-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="c04f1-175">Щелкните **+ Добавить параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="c04f1-176">![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="c04f1-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="c04f1-177">На странице **Единый вход** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c04f1-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="c04f1-178">![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="c04f1-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="c04f1-179">а.</span><span class="sxs-lookup"><span data-stu-id="c04f1-179">a.</span></span> <span data-ttu-id="c04f1-180">В текстовом поле **Имя** введите имя конфигурации (например, *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="c04f1-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="c04f1-181">b.</span><span class="sxs-lookup"><span data-stu-id="c04f1-181">b.</span></span> <span data-ttu-id="c04f1-182">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-182">Select **Enabled**.</span></span>

    <span data-ttu-id="c04f1-183">c.</span><span class="sxs-lookup"><span data-stu-id="c04f1-183">c.</span></span> <span data-ttu-id="c04f1-184">Установите флажок **Использовать новый сертификат единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="c04f1-185">д.</span><span class="sxs-lookup"><span data-stu-id="c04f1-185">e.</span></span> <span data-ttu-id="c04f1-186">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="c04f1-187">Е.</span><span class="sxs-lookup"><span data-stu-id="c04f1-187">f.</span></span> <span data-ttu-id="c04f1-188">Вставьте значение **Идентификатор сущности SAML**, скопированное на портале Azure, в поле **Идентификатор сущности**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="c04f1-189">g.</span><span class="sxs-lookup"><span data-stu-id="c04f1-189">g.</span></span> <span data-ttu-id="c04f1-190">Вставьте значение **URL-адреса службы единого входа SAML**, скопированное с портала Azure, в поле **URL-адрес единого входа** поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c04f1-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="c04f1-191">h.</span><span class="sxs-lookup"><span data-stu-id="c04f1-191">h.</span></span> <span data-ttu-id="c04f1-192">Вставьте значение **URL-адреса выхода**, скопированное с портала Azure, в поле **URL-адрес выхода поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="c04f1-193">i.</span><span class="sxs-lookup"><span data-stu-id="c04f1-193">i.</span></span> <span data-ttu-id="c04f1-194">В поле **SAML User ID Type** (Тип идентификатора пользователя SAML) выберите значение **Assertion contains User”s sprinklr.com username** (Утверждение содержит имя пользователя sprinklr.com).</span><span class="sxs-lookup"><span data-stu-id="c04f1-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="c04f1-195">j.</span><span class="sxs-lookup"><span data-stu-id="c04f1-195">j.</span></span> <span data-ttu-id="c04f1-196">В поле **SAML User ID Location** (Расположение идентификатора пользователя SAML) выберите значение **User ID is in the Name Identifier element of the Subject statement** (Идентификатор пользователя находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="c04f1-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="c04f1-197">k.</span><span class="sxs-lookup"><span data-stu-id="c04f1-197">k.</span></span> <span data-ttu-id="c04f1-198">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-198">Click **Save**.</span></span>
       
    <span data-ttu-id="c04f1-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="c04f1-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="c04f1-200">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c04f1-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c04f1-201">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c04f1-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c04f1-202">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c04f1-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c04f1-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04f1-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="c04f1-204">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c04f1-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c04f1-206">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c04f1-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c04f1-207">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c04f1-209">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c04f1-211">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c04f1-213">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c04f1-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c04f1-215">а.</span><span class="sxs-lookup"><span data-stu-id="c04f1-215">a.</span></span> <span data-ttu-id="c04f1-216">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c04f1-217">b.</span><span class="sxs-lookup"><span data-stu-id="c04f1-217">b.</span></span> <span data-ttu-id="c04f1-218">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c04f1-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c04f1-219">c.</span><span class="sxs-lookup"><span data-stu-id="c04f1-219">c.</span></span> <span data-ttu-id="c04f1-220">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c04f1-221">d.</span><span class="sxs-lookup"><span data-stu-id="c04f1-221">d.</span></span> <span data-ttu-id="c04f1-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="c04f1-223">Создание тестового пользователя Skilljar</span><span class="sxs-lookup"><span data-stu-id="c04f1-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="c04f1-224">Войдите на сайт Sprinklr своей организации в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c04f1-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="c04f1-225">Выберите **Administration (Администрирование) \> Settings (Параметры)**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="c04f1-226">![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="c04f1-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="c04f1-227">В области слева выберите **Manage Client (Управление клиентом) \> Users (Пользователи)**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="c04f1-228">![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="c04f1-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="c04f1-229">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="c04f1-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="c04f1-230">![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="c04f1-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="c04f1-231">В диалоговом окне **Изменение пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c04f1-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c04f1-232">![Изменение пользователя](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="c04f1-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="c04f1-233">а.</span><span class="sxs-lookup"><span data-stu-id="c04f1-233">a.</span></span> <span data-ttu-id="c04f1-234">В текстовых полях **Email** (Электронная почта), **First Name** (Имя) и **Last Name** (Фамилия) введите данные учетной записи пользователя Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="c04f1-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="c04f1-235">b.</span><span class="sxs-lookup"><span data-stu-id="c04f1-235">b.</span></span> <span data-ttu-id="c04f1-236">Установите флажок **Пароль отключен**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="c04f1-237">c.</span><span class="sxs-lookup"><span data-stu-id="c04f1-237">c.</span></span> <span data-ttu-id="c04f1-238">Выберите **Язык**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-238">Select **Language**.</span></span>

    <span data-ttu-id="c04f1-239">г)</span><span class="sxs-lookup"><span data-stu-id="c04f1-239">d.</span></span> <span data-ttu-id="c04f1-240">Выберите **Тип пользователя**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-240">Select **User Type**.</span></span>

    <span data-ttu-id="c04f1-241">д.</span><span class="sxs-lookup"><span data-stu-id="c04f1-241">e.</span></span> <span data-ttu-id="c04f1-242">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="c04f1-243">**Пароль отключен** , чтобы дать пользователю возможность входить через поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c04f1-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="c04f1-244">Перейдите в раздел **Роль**и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c04f1-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="c04f1-245">![Роли партнера](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Роли партнера")</span><span class="sxs-lookup"><span data-stu-id="c04f1-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="c04f1-246">а.</span><span class="sxs-lookup"><span data-stu-id="c04f1-246">a.</span></span> <span data-ttu-id="c04f1-247">В списке **Global** (Глобальные) выберите **ALL\_Permissions**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="c04f1-248">b.</span><span class="sxs-lookup"><span data-stu-id="c04f1-248">b.</span></span> <span data-ttu-id="c04f1-249">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="c04f1-250">Вы можете использовать любые другие инструменты создания учетных записей пользователей Sprinklr или API, предоставляемые Sprinklr для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="c04f1-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c04f1-251">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04f1-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c04f1-252">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="c04f1-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c04f1-254">**Чтобы назначить пользователя Britta Simon для Sprinklr, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c04f1-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="c04f1-255">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c04f1-257">В списке приложений выберите **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-257">In the applications list, select **Sprinklr**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="c04f1-259">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c04f1-261">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-261">Click **Add** button.</span></span> <span data-ttu-id="c04f1-262">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c04f1-264">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c04f1-265">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c04f1-266">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c04f1-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c04f1-267">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c04f1-267">Testing single sign-on</span></span>

<span data-ttu-id="c04f1-268">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c04f1-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c04f1-269">Щелкнув элемент Sprinklr на панели доступа, вы автоматически войдете в приложение Sprinklr. Дополнительные сведения о панели доступа см. в разделе [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c04f1-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c04f1-270">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c04f1-270">Additional resources</span></span>

* [<span data-ttu-id="c04f1-271">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c04f1-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c04f1-272">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c04f1-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

