---
title: "Учебник. Интеграция Azure Active Directory с LogicMonitor | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="6df4e-103">Руководство. Интеграция Azure Active Directory с LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="6df4e-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="6df4e-104">В этом руководстве описано, как интегрировать LogicMonitor с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6df4e-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6df4e-105">Интеграция Azure AD с приложением LogicMonitor обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="6df4e-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6df4e-106">С помощью Azure AD можно управлять доступом к LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="6df4e-107">Вы можете включить автоматический вход пользователей в LogicMonitor (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df4e-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6df4e-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6df4e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6df4e-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6df4e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6df4e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6df4e-110">Prerequisites</span></span>

<span data-ttu-id="6df4e-111">Чтобы настроить интеграцию Azure AD с LogicMonitor, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="6df4e-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="6df4e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6df4e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6df4e-113">подписка LogicMonitor с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6df4e-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6df4e-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="6df4e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6df4e-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="6df4e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6df4e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6df4e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6df4e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6df4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6df4e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6df4e-118">Scenario description</span></span>
<span data-ttu-id="6df4e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6df4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6df4e-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="6df4e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6df4e-121">Добавление LogicMonitor из коллекции</span><span class="sxs-lookup"><span data-stu-id="6df4e-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="6df4e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df4e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="6df4e-123">Добавление LogicMonitor из коллекции</span><span class="sxs-lookup"><span data-stu-id="6df4e-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="6df4e-124">Чтобы настроить интеграцию LogicMonitor с Azure AD, необходимо добавить LogicMonitor из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6df4e-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6df4e-125">**Чтобы добавить LogicMonitor из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="6df4e-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6df4e-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6df4e-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6df4e-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6df4e-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6df4e-133">В поле поиска введите **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-133">In the search box, type **LogicMonitor**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="6df4e-135">На панели результатов выберите **LogicMonitor**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="6df4e-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6df4e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df4e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6df4e-138">В этом разделе описана настройка и проверка единого входа Azure AD в LogicMonitor с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6df4e-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6df4e-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в LogicMonitor соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df4e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="6df4e-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="6df4e-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6df4e-142">Чтобы настроить и проверить единый вход Azure AD в LogicMonitor, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="6df4e-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6df4e-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="6df4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6df4e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6df4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6df4e-145">**[Создание тестового пользователя LogicMonitor](#creating-a-logicmonitor-test-user)** требуется для создания в LogicMonitor пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df4e-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6df4e-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6df4e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6df4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6df4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6df4e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df4e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6df4e-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="6df4e-150">**Чтобы настроить единый вход Azure AD в LogicMonitor, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="6df4e-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="6df4e-151">На портале Azure на странице интеграции с приложением **LogicMonitor** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6df4e-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="6df4e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="6df4e-155">В разделе **Домен и URL-адреса приложения LogicMonitor** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6df4e-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="6df4e-157">а.</span><span class="sxs-lookup"><span data-stu-id="6df4e-157">a.</span></span> <span data-ttu-id="6df4e-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="6df4e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="6df4e-159">b.</span><span class="sxs-lookup"><span data-stu-id="6df4e-159">b.</span></span> <span data-ttu-id="6df4e-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="6df4e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6df4e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6df4e-161">These values are not real.</span></span> <span data-ttu-id="6df4e-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="6df4e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6df4e-163">Чтобы получить их, обратитесь в [службу поддержки клиентов LogicMonitor](https://www.logicmonitor.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6df4e-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="6df4e-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6df4e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="6df4e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6df4e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6df4e-168">Выполните вход на веб-сайт компании **LogicMonitor** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="6df4e-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="6df4e-169">В верхнем меню нажмите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="6df4e-170">![Параметры](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="6df4e-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="6df4e-171">В расположенной слева области навигации нажмите **Единый вход**</span><span class="sxs-lookup"><span data-stu-id="6df4e-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="6df4e-172">![Единый вход](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="6df4e-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="6df4e-173">В разделе **Параметры единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6df4e-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6df4e-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings") (Параметры единого входа)</span><span class="sxs-lookup"><span data-stu-id="6df4e-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="6df4e-175">а.</span><span class="sxs-lookup"><span data-stu-id="6df4e-175">a.</span></span> <span data-ttu-id="6df4e-176">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="6df4e-177">b.</span><span class="sxs-lookup"><span data-stu-id="6df4e-177">b.</span></span> <span data-ttu-id="6df4e-178">Выберите для параметра **Default Role Assignment** (Назначение ролей по умолчанию) значение **readonly** (только для чтения).</span><span class="sxs-lookup"><span data-stu-id="6df4e-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="6df4e-179">c.</span><span class="sxs-lookup"><span data-stu-id="6df4e-179">c.</span></span> <span data-ttu-id="6df4e-180">Откройте скачанный файл метаданных в Блокноте и вставьте содержимое этого файла в текстовое поле **Метаданные поставщика удостоверений** .</span><span class="sxs-lookup"><span data-stu-id="6df4e-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="6df4e-181">г)</span><span class="sxs-lookup"><span data-stu-id="6df4e-181">d.</span></span> <span data-ttu-id="6df4e-182">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6df4e-183">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="6df4e-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6df4e-184">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="6df4e-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6df4e-185">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="6df4e-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6df4e-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df4e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="6df4e-187">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6df4e-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6df4e-189">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6df4e-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6df4e-190">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6df4e-192">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6df4e-194">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6df4e-196">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6df4e-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6df4e-198">а.</span><span class="sxs-lookup"><span data-stu-id="6df4e-198">a.</span></span> <span data-ttu-id="6df4e-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6df4e-200">b.</span><span class="sxs-lookup"><span data-stu-id="6df4e-200">b.</span></span> <span data-ttu-id="6df4e-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6df4e-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6df4e-202">c.</span><span class="sxs-lookup"><span data-stu-id="6df4e-202">c.</span></span> <span data-ttu-id="6df4e-203">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6df4e-204">d.</span><span class="sxs-lookup"><span data-stu-id="6df4e-204">d.</span></span> <span data-ttu-id="6df4e-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="6df4e-206">Создание тестового пользователя LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="6df4e-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="6df4e-207">Чтобы пользователи AAD могли войти систему, они должны быть подготовлены для приложения LogicMonitor с использованием их имен пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6df4e-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="6df4e-208">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="6df4e-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6df4e-209">Выполните вход на веб-сайт компании LogicMonitor в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="6df4e-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="6df4e-210">В меню вверху щелкните **Settings** (Параметры), а затем выберите **Roles and Users** (Роли и пользователи).</span><span class="sxs-lookup"><span data-stu-id="6df4e-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="6df4e-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users") (Роли и пользователи)</span><span class="sxs-lookup"><span data-stu-id="6df4e-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="6df4e-212">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-212">Click **Add**.</span></span>

4. <span data-ttu-id="6df4e-213">В разделе **Добавить учетную запись** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6df4e-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6df4e-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account") (Добавление учетной записи)</span><span class="sxs-lookup"><span data-stu-id="6df4e-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="6df4e-215">а.</span><span class="sxs-lookup"><span data-stu-id="6df4e-215">a.</span></span> <span data-ttu-id="6df4e-216">В соответствующие текстовые поля введите значения **имени пользователя**, **адреса электронной почты**, **пароля** и **подтверждения пароля** пользователя Azure Active Directory, которого требуется подготовить.</span><span class="sxs-lookup"><span data-stu-id="6df4e-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="6df4e-217">b.</span><span class="sxs-lookup"><span data-stu-id="6df4e-217">b.</span></span> <span data-ttu-id="6df4e-218">Выберите **Роли**, **Просмотр разрешений** и **Состояние**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="6df4e-219">c.</span><span class="sxs-lookup"><span data-stu-id="6df4e-219">c.</span></span> <span data-ttu-id="6df4e-220">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="6df4e-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="6df4e-221">Вы можете использовать любые другие средства создания учетной записи пользователя LogicMonitor или API, предоставляемые LogicMonitor для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6df4e-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6df4e-222">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6df4e-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6df4e-223">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6df4e-225">**Чтобы назначить пользователя Britta Simon приложению LogicMonitor, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="6df4e-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="6df4e-226">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6df4e-228">В списке приложений выберите **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="6df4e-230">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6df4e-232">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-232">Click **Add** button.</span></span> <span data-ttu-id="6df4e-233">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6df4e-235">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6df4e-236">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6df4e-237">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6df4e-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6df4e-238">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6df4e-238">Testing single sign-on</span></span>

<span data-ttu-id="6df4e-239">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="6df4e-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="6df4e-240">Щелкнув плитку LogicMonitor на панели доступа, вы автоматически войдете в приложение LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6df4e-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="6df4e-241">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6df4e-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6df4e-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6df4e-242">Additional resources</span></span>

* [<span data-ttu-id="6df4e-243">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6df4e-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6df4e-244">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6df4e-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

