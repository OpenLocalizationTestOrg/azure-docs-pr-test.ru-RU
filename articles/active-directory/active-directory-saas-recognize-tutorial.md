---
title: "Руководство по интеграции Azure Active Directory с Recognize | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Recognize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="faa5e-103">Руководство по интеграции Azure Active Directory с Recognize</span><span class="sxs-lookup"><span data-stu-id="faa5e-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="faa5e-104">В этом руководстве описано, как интегрировать Recognize с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="faa5e-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="faa5e-105">Интеграция Recognize с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="faa5e-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="faa5e-106">с помощью Azure AD вы можете контролировать доступ к Recognize;</span><span class="sxs-lookup"><span data-stu-id="faa5e-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="faa5e-107">вы можете включить автоматический вход пользователей в Recognize (единый вход) под учетной записью Azure AD;</span><span class="sxs-lookup"><span data-stu-id="faa5e-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="faa5e-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="faa5e-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="faa5e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faa5e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="faa5e-110">Prerequisites</span></span>

<span data-ttu-id="faa5e-111">Чтобы настроить интеграцию Azure AD с Recognize, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="faa5e-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="faa5e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="faa5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="faa5e-113">подписка Recognize с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="faa5e-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="faa5e-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="faa5e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="faa5e-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="faa5e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="faa5e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="faa5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="faa5e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="faa5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="faa5e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="faa5e-118">Scenario description</span></span>
<span data-ttu-id="faa5e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="faa5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="faa5e-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="faa5e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="faa5e-121">Добавление Recognize из коллекции.</span><span class="sxs-lookup"><span data-stu-id="faa5e-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="faa5e-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="faa5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="faa5e-123">Добавление Recognize из коллекции</span><span class="sxs-lookup"><span data-stu-id="faa5e-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="faa5e-124">Чтобы настроить интеграцию Recognize с Azure AD, необходимо добавить Recognize из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="faa5e-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="faa5e-125">**Чтобы добавить Recognize из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="faa5e-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="faa5e-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="faa5e-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="faa5e-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="faa5e-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="faa5e-133">В поле поиска введите **Recognize** .</span><span class="sxs-lookup"><span data-stu-id="faa5e-133">In the search box, type **Recognize**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="faa5e-135">На панели результатов выберите **Recognize** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="faa5e-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="faa5e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="faa5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="faa5e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Recognize с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="faa5e-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="faa5e-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Recognize соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="faa5e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="faa5e-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="faa5e-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="faa5e-142">Чтобы настроить и проверить единый вход Azure AD в Recognize, вам потребуется выполнить следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="faa5e-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="faa5e-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="faa5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="faa5e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="faa5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="faa5e-145">**[Создание тестового пользователя Recognize](#creating-a-recognize-test-user)** требуется для того, чтобы в Recognize существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="faa5e-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="faa5e-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="faa5e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="faa5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="faa5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="faa5e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="faa5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="faa5e-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="faa5e-150">**Чтобы настроить единый вход Azure AD в Recognize, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="faa5e-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="faa5e-151">На портале Azure на странице интеграции с приложением **Recognize** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="faa5e-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="faa5e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="faa5e-155">В разделе **Домены и URL-адреса приложения Recognize** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="faa5e-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="faa5e-157">а.</span><span class="sxs-lookup"><span data-stu-id="faa5e-157">a.</span></span> <span data-ttu-id="faa5e-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="faa5e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="faa5e-159">b.</span><span class="sxs-lookup"><span data-stu-id="faa5e-159">b.</span></span> <span data-ttu-id="faa5e-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="faa5e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="faa5e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="faa5e-161">These values are not real.</span></span> <span data-ttu-id="faa5e-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="faa5e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="faa5e-163">Обратитесь к [группе поддержки клиентов Recognize](mailto:support@recognizeapp.com), чтобы получить URL-адрес входа. Чтобы получить значение идентификатора, можно открыть URL-адрес метаданных поставщика услуг из раздела параметров единого входа, как описано далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faa5e-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="faa5e-164">.</span><span class="sxs-lookup"><span data-stu-id="faa5e-164">.</span></span> 
 
4. <span data-ttu-id="faa5e-165">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="faa5e-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="faa5e-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="faa5e-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="faa5e-169">В разделе **Конфигурация Recognize** щелкните **Настроить Recognize**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="faa5e-170">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="faa5e-172">В другом окне веб-браузера войдите на корпоративный сайт Recognize с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="faa5e-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="faa5e-173">В правом верхнем углу щелкните **Menu** (Меню).</span><span class="sxs-lookup"><span data-stu-id="faa5e-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="faa5e-174">Перейдите к пункту **Company Admin** (Администратор компании).</span><span class="sxs-lookup"><span data-stu-id="faa5e-174">Go to **Company Admin**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="faa5e-176">В левой панели навигации щелкните **Settings**(Параметры).</span><span class="sxs-lookup"><span data-stu-id="faa5e-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="faa5e-178">В разделе **SSO Settings** (Параметры единого входа) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="faa5e-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="faa5e-180">а.</span><span class="sxs-lookup"><span data-stu-id="faa5e-180">a.</span></span> <span data-ttu-id="faa5e-181">Для параметра **Enable SSO** (Включить единый вход) установите значение **ON** (Включено).</span><span class="sxs-lookup"><span data-stu-id="faa5e-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="faa5e-182">b.</span><span class="sxs-lookup"><span data-stu-id="faa5e-182">b.</span></span> <span data-ttu-id="faa5e-183">В текстовое поле **IDP Entity ID** (Идентификатор сущности IdP) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5e-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="faa5e-184">c.</span><span class="sxs-lookup"><span data-stu-id="faa5e-184">c.</span></span> <span data-ttu-id="faa5e-185">В текстовое поле **Sso target url** (Целевой URL-адрес единого входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5e-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="faa5e-186">г)</span><span class="sxs-lookup"><span data-stu-id="faa5e-186">d.</span></span> <span data-ttu-id="faa5e-187">В текстовое поле **Slo target url** (Целевой URL-адрес единого выхода) вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5e-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="faa5e-188">д.</span><span class="sxs-lookup"><span data-stu-id="faa5e-188">e.</span></span> <span data-ttu-id="faa5e-189">Откройте скачанный файл **сертификата в кодировке Base64** в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Certificate** (Сертификат).</span><span class="sxs-lookup"><span data-stu-id="faa5e-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="faa5e-190">f.</span><span class="sxs-lookup"><span data-stu-id="faa5e-190">f.</span></span> <span data-ttu-id="faa5e-191">Нажмите кнопку **Сохранить параметры** .</span><span class="sxs-lookup"><span data-stu-id="faa5e-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="faa5e-192">Кроме сведений в разделе **SSO Settings** (Параметры единого входа), сохраните URL-адрес из раздела **Service Provider Metadata url** (URL-адрес метаданных поставщика службы).</span><span class="sxs-lookup"><span data-stu-id="faa5e-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="faa5e-194">Откройте ссылку с **URL-адресом метаданных** в новом окне браузера, чтобы скачать документ метаданных.</span><span class="sxs-lookup"><span data-stu-id="faa5e-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="faa5e-195">Затем скопируйте значение EntityDescriptor (entityID) из файла и вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения Recognize** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5e-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="faa5e-197">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="faa5e-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="faa5e-198">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="faa5e-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="faa5e-199">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="faa5e-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="faa5e-200">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="faa5e-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="faa5e-201">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="faa5e-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="faa5e-203">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="faa5e-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="faa5e-204">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="faa5e-206">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="faa5e-208">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="faa5e-210">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="faa5e-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="faa5e-212">а.</span><span class="sxs-lookup"><span data-stu-id="faa5e-212">a.</span></span> <span data-ttu-id="faa5e-213">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="faa5e-214">b.</span><span class="sxs-lookup"><span data-stu-id="faa5e-214">b.</span></span> <span data-ttu-id="faa5e-215">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="faa5e-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="faa5e-216">c.</span><span class="sxs-lookup"><span data-stu-id="faa5e-216">c.</span></span> <span data-ttu-id="faa5e-217">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="faa5e-218">d.</span><span class="sxs-lookup"><span data-stu-id="faa5e-218">d.</span></span> <span data-ttu-id="faa5e-219">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="faa5e-220">Создание тестового пользователя Recognize</span><span class="sxs-lookup"><span data-stu-id="faa5e-220">Creating a Recognize test user</span></span>

<span data-ttu-id="faa5e-221">Чтобы пользователи Azure AD могли выполнять вход в Recognize, они должны быть подготовлены для Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="faa5e-222">Для Recognize подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="faa5e-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="faa5e-223">Это приложение не поддерживает подготовку SCIM, но предусматривает альтернативный механизм синхронизации для подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="faa5e-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="faa5e-224">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="faa5e-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="faa5e-225">Войдите на корпоративный сайт Recognize в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="faa5e-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="faa5e-226">В правом верхнем углу щелкните **Menu** (Меню).</span><span class="sxs-lookup"><span data-stu-id="faa5e-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="faa5e-227">Перейдите к пункту **Company Admin** (Администратор компании).</span><span class="sxs-lookup"><span data-stu-id="faa5e-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="faa5e-228">В левой панели навигации щелкните **Settings**(Параметры).</span><span class="sxs-lookup"><span data-stu-id="faa5e-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="faa5e-229">В разделе **User Sync** (Синхронизация пользователей) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="faa5e-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="faa5e-230">![Новый пользователь](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="faa5e-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="faa5e-231">а.</span><span class="sxs-lookup"><span data-stu-id="faa5e-231">a.</span></span> <span data-ttu-id="faa5e-232">В поле **Sync Enabled** (Синхронизация включена) выберите **ON** (Включено).</span><span class="sxs-lookup"><span data-stu-id="faa5e-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="faa5e-233">b.</span><span class="sxs-lookup"><span data-stu-id="faa5e-233">b.</span></span> <span data-ttu-id="faa5e-234">Для параметра **Choose sync provider** (Выбор поставщика синхронизации) выберите значение **Microsoft/Office 365**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="faa5e-235">c.</span><span class="sxs-lookup"><span data-stu-id="faa5e-235">c.</span></span> <span data-ttu-id="faa5e-236">Щелкните **Run User Sync** (Запустить синхронизацию пользователей).</span><span class="sxs-lookup"><span data-stu-id="faa5e-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="faa5e-237">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="faa5e-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="faa5e-238">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="faa5e-240">**Чтобы назначить пользователя Britta Simon в Recognize, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="faa5e-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="faa5e-241">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="faa5e-243">В списке приложений выберите **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-243">In the applications list, select **Recognize**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="faa5e-245">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="faa5e-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-247">Click **Add** button.</span></span> <span data-ttu-id="faa5e-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="faa5e-250">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="faa5e-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="faa5e-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="faa5e-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="faa5e-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="faa5e-253">Testing single sign-on</span></span>

<span data-ttu-id="faa5e-254">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="faa5e-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="faa5e-255">Щелкнув элемент Recognize на панели доступа, вы автоматически войдете в приложение Recognize.</span><span class="sxs-lookup"><span data-stu-id="faa5e-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="faa5e-256">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="faa5e-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="faa5e-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="faa5e-257">Additional resources</span></span>

* [<span data-ttu-id="faa5e-258">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="faa5e-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="faa5e-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="faa5e-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

