---
title: "Руководство по интеграции Azure Active Directory с Panopto | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="8bcd9-103">Учебник. Интеграция Azure Active Directory с Panopto</span><span class="sxs-lookup"><span data-stu-id="8bcd9-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="8bcd9-104">В этом руководстве описано, как интегрировать Panopto с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bcd9-105">Интеграция Azure AD с приложением Panopto обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8bcd9-106">С помощью Azure AD вы можете контролировать доступ к Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="8bcd9-107">Вы можете включить автоматический вход пользователей в Panopto (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bcd9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8bcd9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bcd9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8bcd9-110">Prerequisites</span></span>

<span data-ttu-id="8bcd9-111">Чтобы настроить интеграцию Azure AD с Panopto, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="8bcd9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8bcd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bcd9-113">подписка Panopto с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bcd9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bcd9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bcd9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bcd9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bcd9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8bcd9-118">Scenario description</span></span>
<span data-ttu-id="8bcd9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bcd9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bcd9-121">Добавление Panopto из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="8bcd9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bcd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="8bcd9-123">Добавление Panopto из коллекции</span><span class="sxs-lookup"><span data-stu-id="8bcd9-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="8bcd9-124">Чтобы настроить интеграцию Panopto с Azure AD, необходимо добавить Panopto из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bcd9-125">**Чтобы добавить Panopto из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8bcd9-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bcd9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bcd9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8bcd9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8bcd9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8bcd9-133">В поле поиска введите **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-133">In the search box, type **Panopto**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="8bcd9-135">На панели результатов выберите **Panopto** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bcd9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bcd9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8bcd9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Panopto с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8bcd9-139">Чтобы единый вход работал, Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="8bcd9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="8bcd9-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8bcd9-142">Чтобы настроить и проверить единый вход Azure AD в Panopto, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bcd9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bcd9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bcd9-145">**[Создание тестового пользователя Panopto](#creating-a-panopto-test-user)** требуется для создания в Panopto пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bcd9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bcd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bcd9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bcd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bcd9-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="8bcd9-150">**Чтобы настроить единый вход Azure AD в Panopto, выполните следующее:**</span><span class="sxs-lookup"><span data-stu-id="8bcd9-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="8bcd9-151">На портале Azure на странице интеграции с приложением **Panopto** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8bcd9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="8bcd9-155">В разделе **Домены и URL-адреса приложения Panopto** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="8bcd9-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="8bcd9-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8bcd9-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-158">This value is not real.</span></span> <span data-ttu-id="8bcd9-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8bcd9-160">Для получения этого значения обратитесь в [службу поддержки клиентов Panopto](mailto:support@panopto.com‎).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="8bcd9-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="8bcd9-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8bcd9-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bcd9-165">В разделе **Настройка Panopto** выберите **Настроить Panopto**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8bcd9-166">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="8bcd9-168">В другом окне веб-браузера войдите на сайт Panopto своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="8bcd9-169">На панели слева щелкните **System** (Система), а затем щелкните **Identity Providers** (Поставщики удостоверений).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="8bcd9-170">![Система](./media/active-directory-saas-panopto-tutorial/ic777670.png "Система")</span><span class="sxs-lookup"><span data-stu-id="8bcd9-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="8bcd9-171">Щелкните **Добавить поставщик**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="8bcd9-172">![Поставщики удостоверений](./media/active-directory-saas-panopto-tutorial/ic777671.png "Поставщики удостоверений")</span><span class="sxs-lookup"><span data-stu-id="8bcd9-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="8bcd9-173">В разделе сведений поставщика SAML выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="8bcd9-174">![Конфигурация SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Конфигурация SaaS")</span><span class="sxs-lookup"><span data-stu-id="8bcd9-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="8bcd9-175">а.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-175">a.</span></span> <span data-ttu-id="8bcd9-176">В списке **Provider Type** (Тип поставщика) выберите пункт **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="8bcd9-177">b.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-177">b.</span></span> <span data-ttu-id="8bcd9-178">В текстовом поле **Имя экземпляра** введите имя экземпляра.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="8bcd9-179">c.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-179">c.</span></span> <span data-ttu-id="8bcd9-180">В текстовом поле **Понятное описание** введите понятное описание.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="8bcd9-181">г)</span><span class="sxs-lookup"><span data-stu-id="8bcd9-181">d.</span></span> <span data-ttu-id="8bcd9-182">В текстовое поле **Bounce Page Url** (URL-адрес страницы возврата) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8bcd9-183">д.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-183">e.</span></span> <span data-ttu-id="8bcd9-184">В текстовое поле **Issuer** (Издатель) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8bcd9-185">f.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-185">f.</span></span> <span data-ttu-id="8bcd9-186">Откройте в блокноте сертификат в кодировке Base-64, скачанный на портале Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Public Key** (Открытый ключ).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="8bcd9-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8bcd9-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8bcd9-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8bcd9-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bcd9-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bcd9-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="8bcd9-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8bcd9-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8bcd9-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bcd9-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bcd9-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bcd9-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bcd9-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bcd9-203">а.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-203">a.</span></span> <span data-ttu-id="8bcd9-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bcd9-205">b.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-205">b.</span></span> <span data-ttu-id="8bcd9-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bcd9-207">c.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-207">c.</span></span> <span data-ttu-id="8bcd9-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8bcd9-209">d.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-209">d.</span></span> <span data-ttu-id="8bcd9-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="8bcd9-211">Создание тестового пользователя приложения Panopto</span><span class="sxs-lookup"><span data-stu-id="8bcd9-211">Creating a Panopto test user</span></span>

<span data-ttu-id="8bcd9-212">Действие для настройки подготовки пользователей в Panopto отсутствует.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="8bcd9-213">Когда назначенный пользователь пытается войти в Panopto с помощью панели доступа, Panopto проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="8bcd9-214">Если учетная запись пользователя отсутствует, Panopto автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="8bcd9-215">Вы можете использовать любые другие инструменты создания учетных записей пользователя Panopto или API, предоставляемые Panopto для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8bcd9-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bcd9-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8bcd9-217">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Panopto, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8bcd9-219">**Чтобы назначить пользователя Britta Simon в приложении** , выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8bcd9-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="8bcd9-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8bcd9-222">В списке приложений выберите **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-222">In the applications list, select **Panopto**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="8bcd9-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8bcd9-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-226">Click **Add** button.</span></span> <span data-ttu-id="8bcd9-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8bcd9-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8bcd9-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bcd9-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bcd9-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8bcd9-232">Testing single sign-on</span></span>

<span data-ttu-id="8bcd9-233">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8bcd9-234">Щелкнув элемент Panopto на панели доступа, вы автоматически войдете в приложение Panopto.</span><span class="sxs-lookup"><span data-stu-id="8bcd9-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="8bcd9-235">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8bcd9-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bcd9-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8bcd9-236">Additional resources</span></span>

* [<span data-ttu-id="8bcd9-237">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bcd9-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bcd9-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bcd9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

