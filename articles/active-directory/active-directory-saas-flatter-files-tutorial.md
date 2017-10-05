---
title: "Учебник. Интеграция Azure Active Directory с Flatter Files | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Flatter Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="65dc0-103">Руководство. Интеграция Azure Active Directory с Flatter Files</span><span class="sxs-lookup"><span data-stu-id="65dc0-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="65dc0-104">В этом руководстве описано, как интегрировать приложение Flatter Files с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65dc0-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65dc0-105">Интеграция Azure AD с Flatter Files обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="65dc0-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65dc0-106">С помощью Azure AD вы можете контролировать доступ к Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="65dc0-107">Вы можете включить автоматический вход пользователей в Flatter Files (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65dc0-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65dc0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="65dc0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65dc0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65dc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65dc0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="65dc0-110">Prerequisites</span></span>

<span data-ttu-id="65dc0-111">Чтобы настроить интеграцию Azure AD с Flatter Files, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="65dc0-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="65dc0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="65dc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65dc0-113">подписка с поддержкой единого входа в Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65dc0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="65dc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65dc0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="65dc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65dc0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="65dc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65dc0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65dc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65dc0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="65dc0-118">Scenario description</span></span>
<span data-ttu-id="65dc0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="65dc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65dc0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="65dc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65dc0-121">Добавление Flatter Files из коллекции</span><span class="sxs-lookup"><span data-stu-id="65dc0-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="65dc0-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65dc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="65dc0-123">Добавление Flatter Files из коллекции</span><span class="sxs-lookup"><span data-stu-id="65dc0-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="65dc0-124">Чтобы настроить интеграцию Flatter Files с Azure AD, необходимо добавить Flatter Files из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="65dc0-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65dc0-125">**Как добавить Flatter Files из коллекции**</span><span class="sxs-lookup"><span data-stu-id="65dc0-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65dc0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65dc0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65dc0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="65dc0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="65dc0-133">В поле поиска введите **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-133">In the search box, type **Flatter Files**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="65dc0-135">На панели результатов выберите **Flatter Files** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="65dc0-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65dc0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="65dc0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65dc0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Flatter Files с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65dc0-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65dc0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Flatter Files соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65dc0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="65dc0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="65dc0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65dc0-142">Чтобы настроить и проверить единый вход Azure AD в Flatter Files, вам потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="65dc0-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65dc0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="65dc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65dc0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65dc0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65dc0-145">**[Создание тестового пользователя Flatter Files](#creating-a-flatter-files-test-user)** требуется для создания во Flatter Files пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65dc0-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65dc0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65dc0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65dc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="65dc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65dc0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="65dc0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65dc0-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="65dc0-150">**Как настроить единый вход Azure AD в Flatter Files**</span><span class="sxs-lookup"><span data-stu-id="65dc0-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="65dc0-151">На портале Azure на странице интеграции с приложением **Flatter Files** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="65dc0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="65dc0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="65dc0-155">В разделе **Домен и URL-адреса Flatter Files** не нужно выполнять никаких действий, поскольку приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="65dc0-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="65dc0-157">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="65dc0-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="65dc0-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="65dc0-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65dc0-161">В разделе **Конфигурация Flatter Files** щелкните **Настроить Flatter Files**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65dc0-162">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="65dc0-164">Войдите в приложение Flatter Files с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="65dc0-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="65dc0-165">Щелкните **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-165">Click **DASHBOARD**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="65dc0-167">Выберите элемент **Settings** (Параметры), а затем выполните следующие действия на вкладке **Company** (Компания).</span><span class="sxs-lookup"><span data-stu-id="65dc0-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="65dc0-169">а.</span><span class="sxs-lookup"><span data-stu-id="65dc0-169">a.</span></span> <span data-ttu-id="65dc0-170">Установите флажок **Use SAML 2.0 For Authentication**(Использовать SAML 2.0 для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="65dc0-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="65dc0-171">b.</span><span class="sxs-lookup"><span data-stu-id="65dc0-171">b.</span></span> <span data-ttu-id="65dc0-172">Нажмите кнопку **Configure SAML** (Настроить SAML).</span><span class="sxs-lookup"><span data-stu-id="65dc0-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="65dc0-173">В диалоговом окне **SAML Configuration** (Настройка SAML) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="65dc0-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="65dc0-175">а.</span><span class="sxs-lookup"><span data-stu-id="65dc0-175">a.</span></span> <span data-ttu-id="65dc0-176">В поле **Домен** укажите свой зарегистрированный домен.</span><span class="sxs-lookup"><span data-stu-id="65dc0-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="65dc0-177">Если у вас нет зарегистрированного домена, обратитесь в службу поддержки Flatter Files по адресу [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="65dc0-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="65dc0-178">b.</span><span class="sxs-lookup"><span data-stu-id="65dc0-178">b.</span></span> <span data-ttu-id="65dc0-179">В текстовое поле **URL-адрес поставщика удостоверений** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="65dc0-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="65dc0-180">c.</span><span class="sxs-lookup"><span data-stu-id="65dc0-180">c.</span></span>  <span data-ttu-id="65dc0-181">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="65dc0-182">г)</span><span class="sxs-lookup"><span data-stu-id="65dc0-182">d.</span></span> <span data-ttu-id="65dc0-183">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="65dc0-184">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="65dc0-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65dc0-185">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="65dc0-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65dc0-186">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="65dc0-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65dc0-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="65dc0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="65dc0-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65dc0-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="65dc0-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="65dc0-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65dc0-191">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65dc0-193">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65dc0-195">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65dc0-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="65dc0-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65dc0-199">а.</span><span class="sxs-lookup"><span data-stu-id="65dc0-199">a.</span></span> <span data-ttu-id="65dc0-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65dc0-201">b.</span><span class="sxs-lookup"><span data-stu-id="65dc0-201">b.</span></span> <span data-ttu-id="65dc0-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65dc0-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65dc0-203">c.</span><span class="sxs-lookup"><span data-stu-id="65dc0-203">c.</span></span> <span data-ttu-id="65dc0-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65dc0-205">d.</span><span class="sxs-lookup"><span data-stu-id="65dc0-205">d.</span></span> <span data-ttu-id="65dc0-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="65dc0-207">Создание тестового пользователя Flatter Files</span><span class="sxs-lookup"><span data-stu-id="65dc0-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="65dc0-208">Цель этого раздела — создать пользователя с именем Britta Simon в Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="65dc0-209">**Как создать пользователя с именем Britta Simon в Flatter Files**</span><span class="sxs-lookup"><span data-stu-id="65dc0-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="65dc0-210">Войдите на сайт своей компании в службе **Flatter Files** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="65dc0-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="65dc0-211">В области навигации слева щелкните **Settings** (Параметры), а затем выберите вкладку **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="65dc0-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Создание пользователя Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="65dc0-213">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="65dc0-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="65dc0-214">На странице **Добавление пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="65dc0-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Создание пользователя Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="65dc0-216">а.</span><span class="sxs-lookup"><span data-stu-id="65dc0-216">a.</span></span> <span data-ttu-id="65dc0-217">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="65dc0-218">b.</span><span class="sxs-lookup"><span data-stu-id="65dc0-218">b.</span></span> <span data-ttu-id="65dc0-219">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="65dc0-220">c.</span><span class="sxs-lookup"><span data-stu-id="65dc0-220">c.</span></span> <span data-ttu-id="65dc0-221">В текстовом поле **Email Address** (Адрес электронной почты) введите адрес электронной почты пользователя Britta Simon на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="65dc0-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="65dc0-222">г)</span><span class="sxs-lookup"><span data-stu-id="65dc0-222">d.</span></span> <span data-ttu-id="65dc0-223">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="65dc0-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65dc0-224">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="65dc0-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65dc0-225">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="65dc0-227">**Как назначить пользователя Britta Simon в Flatter Files**</span><span class="sxs-lookup"><span data-stu-id="65dc0-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="65dc0-228">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="65dc0-230">В списке приложений выберите **Flatter Files**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-230">In the applications list, select **Flatter Files**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="65dc0-232">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="65dc0-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-234">Click **Add** button.</span></span> <span data-ttu-id="65dc0-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="65dc0-237">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65dc0-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65dc0-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="65dc0-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65dc0-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="65dc0-240">Testing single sign-on</span></span>

<span data-ttu-id="65dc0-241">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="65dc0-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65dc0-242">Щелкните элемент Flatter Files на панели доступа, чтобы автоматически войти в приложение Flatter Files.</span><span class="sxs-lookup"><span data-stu-id="65dc0-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="65dc0-243">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65dc0-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65dc0-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="65dc0-244">Additional resources</span></span>

* [<span data-ttu-id="65dc0-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65dc0-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65dc0-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65dc0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

