---
title: "Руководство по интеграции Azure Active Directory с Voyance | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="095a1-103">Руководство по интеграции Azure Active Directory с Voyance</span><span class="sxs-lookup"><span data-stu-id="095a1-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="095a1-104">В этом руководстве описано, как интегрировать Voyance с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="095a1-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="095a1-105">Интеграция Azure AD с приложением Voyance обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="095a1-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="095a1-106">С помощью Azure AD вы можете контролировать доступ к Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="095a1-107">Вы можете включить автоматический вход пользователей в Voyance (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="095a1-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="095a1-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="095a1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="095a1-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="095a1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="095a1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="095a1-110">Prerequisites</span></span>

<span data-ttu-id="095a1-111">Чтобы настроить интеграцию Azure AD с Voyance, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="095a1-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="095a1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="095a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="095a1-113">подписка Voyance с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="095a1-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="095a1-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="095a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="095a1-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="095a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="095a1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="095a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="095a1-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="095a1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="095a1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="095a1-118">Scenario description</span></span>
<span data-ttu-id="095a1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="095a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="095a1-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="095a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="095a1-121">Добавление Voyance из коллекции</span><span class="sxs-lookup"><span data-stu-id="095a1-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="095a1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="095a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="095a1-123">Добавление Voyance из коллекции</span><span class="sxs-lookup"><span data-stu-id="095a1-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="095a1-124">Чтобы настроить интеграцию Voyance с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="095a1-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="095a1-125">**Чтобы добавить Voyance из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="095a1-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="095a1-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="095a1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="095a1-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="095a1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="095a1-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="095a1-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="095a1-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="095a1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="095a1-133">В поле поиска введите **Voyance**, выберите **Voyance** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="095a1-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance в списке результатов](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="095a1-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="095a1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="095a1-136">В этом разделе описана настройка и проверка единого входа Azure AD в Voyance с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="095a1-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="095a1-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Voyance соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="095a1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="095a1-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="095a1-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="095a1-140">Чтобы настроить и проверить единый вход Azure AD в Voyance, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="095a1-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="095a1-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="095a1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="095a1-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="095a1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="095a1-143">**[Создание тестового пользователя Voyance](#create-a-voyance-test-user)** требуется для того, чтобы в Voyance существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="095a1-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="095a1-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="095a1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="095a1-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="095a1-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="095a1-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="095a1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="095a1-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="095a1-148">**Чтобы настроить единый вход Azure AD в Voyance, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="095a1-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="095a1-149">На портале Azure на странице интеграции с приложением **Voyance** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="095a1-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="095a1-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="095a1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="095a1-153">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, в разделе **Домены и URL-адреса приложения Voyance** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="095a1-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика удостоверений](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="095a1-155">а.</span><span class="sxs-lookup"><span data-stu-id="095a1-155">a.</span></span> <span data-ttu-id="095a1-156">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="095a1-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="095a1-157">b.</span><span class="sxs-lookup"><span data-stu-id="095a1-157">b.</span></span> <span data-ttu-id="095a1-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.nyansa.com/saml/create/`.</span><span class="sxs-lookup"><span data-stu-id="095a1-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="095a1-159">Установите флажок **Показать дополнительные параметры URL-адресов**, и выполните следующее действие, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="095a1-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика услуг](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="095a1-161">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="095a1-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="095a1-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="095a1-162">These values are not real.</span></span> <span data-ttu-id="095a1-163">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="095a1-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="095a1-164">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Voyance](mailto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="095a1-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="095a1-165">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="095a1-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="095a1-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="095a1-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="095a1-169">В разделе **Настройка Voyance** щелкните **Настроить Voyance**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="095a1-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="095a1-170">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="095a1-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="095a1-172">В другом окне веб-браузера войдите в свой клиент Voyance с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="095a1-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="095a1-173">В правом верхнем углу щелкните на панели навигации раскрывающийся список **Acme University**.</span><span class="sxs-lookup"><span data-stu-id="095a1-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Настройка единого входа на стороне приложения. Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="095a1-175">Щелкните **Admin Settings** (Параметры администрирования).</span><span class="sxs-lookup"><span data-stu-id="095a1-175">Click "**Admin Settings**".</span></span>

    ![Настройка единого входа на стороне приложения. Параметры администрирования](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="095a1-177">Щелкните вкладку **User Access** (Доступ пользователей).</span><span class="sxs-lookup"><span data-stu-id="095a1-177">Click "**User Access**" tab.</span></span>

    ![Настройка единого входа на стороне приложения. Доступ пользователей](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="095a1-179">Чтобы настроить Azure AD в качестве поставщика удостоверений (IdP) с использованием SAML 2.0, нажмите кнопку **SSO is disabled** (Единый вход отключен).</span><span class="sxs-lookup"><span data-stu-id="095a1-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Настройка единого входа на стороне приложения. Кнопка SSO is disabled (Единый вход отключен)](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="095a1-181">Перейдите в раздел **SAML v2** и выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="095a1-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Настройка единого входа на стороне приложения. SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="095a1-183">а.</span><span class="sxs-lookup"><span data-stu-id="095a1-183">a.</span></span> <span data-ttu-id="095a1-184">Щелкните **Включено**.</span><span class="sxs-lookup"><span data-stu-id="095a1-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="095a1-185">b.</span><span class="sxs-lookup"><span data-stu-id="095a1-185">b.</span></span> <span data-ttu-id="095a1-186">В текстовое поле **IdP Login URL** (URL-адрес входа IdP) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="095a1-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="095a1-187">c.</span><span class="sxs-lookup"><span data-stu-id="095a1-187">c.</span></span> <span data-ttu-id="095a1-188">Откройте скачанный сертификат в кодировке Base64 с помощью блокнота, скопируйте содержимое файла в буфер обмена, а затем вставьте его в текстовое поле **IdP Cert** (Сертификат IdP).</span><span class="sxs-lookup"><span data-stu-id="095a1-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="095a1-189">d.</span><span class="sxs-lookup"><span data-stu-id="095a1-189">d.</span></span> <span data-ttu-id="095a1-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="095a1-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="095a1-191">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="095a1-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="095a1-192">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="095a1-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="095a1-193">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="095a1-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="095a1-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="095a1-194">Create an Azure AD test user</span></span>

<span data-ttu-id="095a1-195">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="095a1-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="095a1-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="095a1-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="095a1-198">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="095a1-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="095a1-200">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="095a1-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="095a1-202">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="095a1-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="095a1-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="095a1-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="095a1-206">а.</span><span class="sxs-lookup"><span data-stu-id="095a1-206">a.</span></span> <span data-ttu-id="095a1-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="095a1-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="095a1-208">b.</span><span class="sxs-lookup"><span data-stu-id="095a1-208">b.</span></span> <span data-ttu-id="095a1-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="095a1-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="095a1-210">c.</span><span class="sxs-lookup"><span data-stu-id="095a1-210">c.</span></span> <span data-ttu-id="095a1-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="095a1-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="095a1-212">d.</span><span class="sxs-lookup"><span data-stu-id="095a1-212">d.</span></span> <span data-ttu-id="095a1-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="095a1-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="095a1-214">Создание тестового пользователя Voyance</span><span class="sxs-lookup"><span data-stu-id="095a1-214">Create a Voyance test user</span></span>

<span data-ttu-id="095a1-215">Цель этого раздела — создать пользователя с именем Britta Simon в приложении Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="095a1-216">Приложение Voyance поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="095a1-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="095a1-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="095a1-217">There is no action item for you in this section.</span></span> <span data-ttu-id="095a1-218">При попытке получить доступ к приложению Voyance будет создан пользователь (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="095a1-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="095a1-219">Чтобы создать пользователя вручную, обратитесь в [службу поддержки Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="095a1-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="095a1-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="095a1-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="095a1-221">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Назначение роли пользователя][200]

<span data-ttu-id="095a1-223">**Чтобы назначить пользователя Britta Simon в Voyance, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="095a1-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="095a1-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="095a1-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="095a1-226">В списке приложений выберите **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="095a1-226">In the applications list, select **Voyance**.</span></span>

    ![Ссылка на Voyance в списке "Приложения"](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="095a1-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="095a1-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="095a1-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="095a1-230">Click **Add** button.</span></span> <span data-ttu-id="095a1-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="095a1-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="095a1-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="095a1-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="095a1-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="095a1-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="095a1-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="095a1-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="095a1-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="095a1-236">Test single sign-on</span></span>

<span data-ttu-id="095a1-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="095a1-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="095a1-238">Щелкнув элемент Voyance на панели доступа, вы автоматически войдете в приложение Voyance.</span><span class="sxs-lookup"><span data-stu-id="095a1-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="095a1-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="095a1-239">Additional resources</span></span>

* [<span data-ttu-id="095a1-240">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="095a1-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="095a1-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="095a1-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

