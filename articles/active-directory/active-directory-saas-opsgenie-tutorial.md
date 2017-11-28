---
title: "Руководство по интеграции Azure Active Directory с OpsGenie | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="8ec80-103">Руководство. Интеграция Azure Active Directory с OpsGenie</span><span class="sxs-lookup"><span data-stu-id="8ec80-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="8ec80-104">В этом руководстве описано, как интегрировать OpsGenie с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ec80-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ec80-105">Интеграция Azure AD с приложением OpsGenie обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="8ec80-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ec80-106">С помощью Azure AD вы можете контролировать доступ к OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="8ec80-107">Вы можете включить автоматический вход пользователей в OpsGenie (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec80-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ec80-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec80-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8ec80-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ec80-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ec80-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8ec80-110">Prerequisites</span></span>

<span data-ttu-id="8ec80-111">Чтобы настроить интеграцию Azure AD с OpsGenie, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8ec80-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="8ec80-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8ec80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ec80-113">подписка OpsGenie с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8ec80-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ec80-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8ec80-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ec80-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8ec80-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ec80-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8ec80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ec80-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ec80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ec80-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8ec80-118">Scenario description</span></span>
<span data-ttu-id="8ec80-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8ec80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ec80-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8ec80-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ec80-121">Добавление OpsGenie из коллекции</span><span class="sxs-lookup"><span data-stu-id="8ec80-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="8ec80-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="8ec80-123">Добавление OpsGenie из коллекции</span><span class="sxs-lookup"><span data-stu-id="8ec80-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="8ec80-124">Чтобы настроить интеграцию OpsGenie с Azure AD, необходимо добавить OpsGenie из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ec80-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ec80-125">**Чтобы добавить OpsGenie из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8ec80-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec80-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ec80-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ec80-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8ec80-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8ec80-133">В поле поиска введите **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-133">In the search box, type **OpsGenie**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="8ec80-135">На панели результатов выберите **OpsGenie** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8ec80-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ec80-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ec80-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение OpsGenie с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec80-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ec80-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в OpsGenie соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec80-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="8ec80-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="8ec80-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ec80-142">Чтобы настроить и проверить единый вход Azure AD в OpsGenie, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="8ec80-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ec80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8ec80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ec80-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ec80-145">**[Создание тестового пользователя OpsGenie](#creating-a-opsgenie-test-user)** требуется для создания пользователя Britta Simon в OpsGenie, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec80-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ec80-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec80-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ec80-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8ec80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ec80-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ec80-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="8ec80-150">**Чтобы настроить единый вход Azure AD в OpsGenie, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8ec80-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec80-151">На портале Azure на странице интеграции с приложением **OpsGenie** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8ec80-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8ec80-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="8ec80-155">В разделе **Домены и URL-адреса приложения OpsGenie** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8ec80-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="8ec80-157">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="8ec80-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="8ec80-158">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8ec80-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="8ec80-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8ec80-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ec80-162">В разделе **Настройка OpsGenie** щелкните **Настроить OpsGenie**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8ec80-163">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="8ec80-165">Откройте другое окно браузера и войдите в OpsGenie с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8ec80-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="8ec80-166">Щелкните **Параметры** и откройте вкладку **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![Единый вход в OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="8ec80-168">Чтобы включить единый вход, установите флажок **Включено**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-168">To enable SSO, select **Enabled**.</span></span>
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="8ec80-170">В разделе **Поставщик** откройте вкладку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="8ec80-172">На странице диалогового окна Azure Active Directory выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8ec80-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="8ec80-174">а.</span><span class="sxs-lookup"><span data-stu-id="8ec80-174">a.</span></span> <span data-ttu-id="8ec80-175">Вставьте **URL-адреса службы единого входа**, который вы скопировали с портала Azure, в текстовое поле **SAML 2.0 Endpoint** (Конечная точка SAML 2.0).</span><span class="sxs-lookup"><span data-stu-id="8ec80-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="8ec80-176">b.</span><span class="sxs-lookup"><span data-stu-id="8ec80-176">b.</span></span> <span data-ttu-id="8ec80-177">Откройте скачанный сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.500**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="8ec80-178">c.</span><span class="sxs-lookup"><span data-stu-id="8ec80-178">c.</span></span> <span data-ttu-id="8ec80-179">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8ec80-180">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8ec80-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ec80-181">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8ec80-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ec80-182">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8ec80-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ec80-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec80-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ec80-184">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec80-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8ec80-186">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8ec80-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec80-187">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ec80-189">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ec80-191">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ec80-193">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8ec80-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ec80-195">а.</span><span class="sxs-lookup"><span data-stu-id="8ec80-195">a.</span></span> <span data-ttu-id="8ec80-196">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ec80-197">b.</span><span class="sxs-lookup"><span data-stu-id="8ec80-197">b.</span></span> <span data-ttu-id="8ec80-198">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ec80-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ec80-199">c.</span><span class="sxs-lookup"><span data-stu-id="8ec80-199">c.</span></span> <span data-ttu-id="8ec80-200">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8ec80-201">d.</span><span class="sxs-lookup"><span data-stu-id="8ec80-201">d.</span></span> <span data-ttu-id="8ec80-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="8ec80-203">Создание тестового пользователя OpsGenie</span><span class="sxs-lookup"><span data-stu-id="8ec80-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="8ec80-204">Цель этого раздела — создать пользователя с именем Britta Simon в OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="8ec80-205">В окне веб-браузера войдите в клиент OpsGenie с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8ec80-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="8ec80-206">Перейдите к списку пользователей, щелкнув **Пользователь** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="8ec80-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="8ec80-208">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="8ec80-208">Click **Add User**.</span></span>

4. <span data-ttu-id="8ec80-209">На странице **Добавление пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8ec80-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="8ec80-211">а.</span><span class="sxs-lookup"><span data-stu-id="8ec80-211">a.</span></span> <span data-ttu-id="8ec80-212">В текстовом поле **Email** (Адрес электронной почты) введите адрес электронной почты пользователя Britta Simon в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ec80-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="8ec80-213">b.</span><span class="sxs-lookup"><span data-stu-id="8ec80-213">b.</span></span> <span data-ttu-id="8ec80-214">В текстовом поле **Full Name** (Полное имя) введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="8ec80-215">c.</span><span class="sxs-lookup"><span data-stu-id="8ec80-215">c.</span></span> <span data-ttu-id="8ec80-216">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="8ec80-217">Britta получит по электронной почте инструкции по настройке профиля.</span><span class="sxs-lookup"><span data-stu-id="8ec80-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ec80-218">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec80-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ec80-219">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8ec80-221">**Чтобы назначить пользователя Britta Simon в OpsGenie, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8ec80-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec80-222">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8ec80-224">Из списка приложений выберите **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-224">In the applications list, select **OpsGenie**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="8ec80-226">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8ec80-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-228">Click **Add** button.</span></span> <span data-ttu-id="8ec80-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8ec80-231">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ec80-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ec80-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8ec80-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ec80-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8ec80-234">Testing single sign-on</span></span>

<span data-ttu-id="8ec80-235">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8ec80-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8ec80-236">Щелкнув элемент OpsGenie на панели доступа, вы автоматически войдете в приложение OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="8ec80-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ec80-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8ec80-237">Additional resources</span></span>

* [<span data-ttu-id="8ec80-238">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ec80-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ec80-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ec80-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

