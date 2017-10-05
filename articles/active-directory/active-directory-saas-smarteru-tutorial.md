---
title: "Руководство по интеграции Azure Active Directory с SmarterU | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="e5f19-103">Учебник. Интеграция Azure Active Directory со SmarterU</span><span class="sxs-lookup"><span data-stu-id="e5f19-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="e5f19-104">В этом учебнике описано, как интегрировать SmarterU с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5f19-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5f19-105">Интеграция Azure AD с приложением SmarterU обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e5f19-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5f19-106">С помощью Azure AD можно управлять доступом к SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="e5f19-107">Вы можете включить автоматический вход пользователей в SmarterU (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5f19-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5f19-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f19-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e5f19-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5f19-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5f19-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e5f19-110">Prerequisites</span></span>

<span data-ttu-id="e5f19-111">Чтобы настроить интеграцию Azure AD с SmarterU, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e5f19-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="e5f19-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e5f19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5f19-113">подписка SmarterU с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e5f19-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5f19-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e5f19-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5f19-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e5f19-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5f19-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e5f19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5f19-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5f19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5f19-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e5f19-118">Scenario description</span></span>
<span data-ttu-id="e5f19-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e5f19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5f19-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e5f19-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5f19-121">Добавление SmarterU из коллекции</span><span class="sxs-lookup"><span data-stu-id="e5f19-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="e5f19-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5f19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="e5f19-123">Добавление SmarterU из коллекции</span><span class="sxs-lookup"><span data-stu-id="e5f19-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="e5f19-124">Чтобы настроить интеграцию SmarterU с Azure AD, необходимо добавить SmarterU из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5f19-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5f19-125">**Чтобы добавить SmarterU из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e5f19-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5f19-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5f19-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5f19-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e5f19-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e5f19-133">В поле поиска введите **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-133">In the search box, type **SmarterU**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="e5f19-135">На панели результатов выберите **SmarterU** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e5f19-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5f19-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5f19-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5f19-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение SmarterU с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5f19-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e5f19-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="e5f19-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="e5f19-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5f19-142">Чтобы настроить и проверить единый вход Azure AD в SmarterU, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e5f19-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5f19-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e5f19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5f19-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5f19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5f19-145">**[Создание тестового пользователя SmarterU](#creating-a-smarteru-test-user)** требуется для создания в SmarterU пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5f19-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5f19-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5f19-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5f19-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e5f19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5f19-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5f19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5f19-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="e5f19-150">**Чтобы настроить единый вход Azure AD в SmarterU, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e5f19-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="e5f19-151">На портале Azure на странице интеграции с приложением **SmarterU** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e5f19-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e5f19-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="e5f19-155">В разделе **Домен и URL-адреса приложения SmarterU** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e5f19-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="e5f19-157">В текстовом поле **Идентификатор** введите URL-адрес: `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="e5f19-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="e5f19-158">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e5f19-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="e5f19-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e5f19-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5f19-162">В другом окне веб-браузера войдите на сайт SmarterU своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e5f19-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="e5f19-163">На панели инструментов вверху щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="e5f19-164">![Параметры учетной записи](./media/active-directory-saas-smarteru-tutorial/IC777326.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="e5f19-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="e5f19-165">На странице конфигурации учетной записи выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e5f19-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="e5f19-166">![Внешняя авторизация](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Внешняя авторизация")</span><span class="sxs-lookup"><span data-stu-id="e5f19-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="e5f19-167">а.</span><span class="sxs-lookup"><span data-stu-id="e5f19-167">a.</span></span> <span data-ttu-id="e5f19-168">Установите флажок **Включить внешнюю авторизацию**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="e5f19-169">b.</span><span class="sxs-lookup"><span data-stu-id="e5f19-169">b.</span></span> <span data-ttu-id="e5f19-170">В разделе **Master Login Control** (Управление универсальным именем для входа) щелкните вкладку **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="e5f19-171">c.</span><span class="sxs-lookup"><span data-stu-id="e5f19-171">c.</span></span> <span data-ttu-id="e5f19-172">В разделе **User Default Login** (Имя для входа пользователей по умолчанию) щелкните вкладку **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="e5f19-173">d.</span><span class="sxs-lookup"><span data-stu-id="e5f19-173">d.</span></span> <span data-ttu-id="e5f19-174">Выберите **Включить Okta**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="e5f19-175">д.</span><span class="sxs-lookup"><span data-stu-id="e5f19-175">e.</span></span> <span data-ttu-id="e5f19-176">Скопируйте содержимое скачанного файла метаданных и вставьте его в текстовое поле **Метаданные Okta** .</span><span class="sxs-lookup"><span data-stu-id="e5f19-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="e5f19-177">Е.</span><span class="sxs-lookup"><span data-stu-id="e5f19-177">f.</span></span> <span data-ttu-id="e5f19-178">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e5f19-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e5f19-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5f19-180">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e5f19-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5f19-181">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e5f19-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5f19-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5f19-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5f19-183">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5f19-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e5f19-185">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e5f19-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5f19-186">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5f19-188">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5f19-190">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5f19-192">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e5f19-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5f19-194">а.</span><span class="sxs-lookup"><span data-stu-id="e5f19-194">a.</span></span> <span data-ttu-id="e5f19-195">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5f19-196">b.</span><span class="sxs-lookup"><span data-stu-id="e5f19-196">b.</span></span> <span data-ttu-id="e5f19-197">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e5f19-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5f19-198">c.</span><span class="sxs-lookup"><span data-stu-id="e5f19-198">c.</span></span> <span data-ttu-id="e5f19-199">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e5f19-200">d.</span><span class="sxs-lookup"><span data-stu-id="e5f19-200">d.</span></span> <span data-ttu-id="e5f19-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="e5f19-202">Создание тестового пользователя SmarterU</span><span class="sxs-lookup"><span data-stu-id="e5f19-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="e5f19-203">Чтобы пользователи Azure AD могли входить в SmarterU, их необходимо подготовить в SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="e5f19-204">В случае SmarterU подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e5f19-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="e5f19-205">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e5f19-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e5f19-206">Выполните вход в клиент **SmarterU** .</span><span class="sxs-lookup"><span data-stu-id="e5f19-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="e5f19-207">Перейдите в раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-207">Go to **Users**.</span></span>

3. <span data-ttu-id="e5f19-208">В разделе «Пользователи» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e5f19-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="e5f19-209">![Новый пользователь](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="e5f19-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="e5f19-210">а.</span><span class="sxs-lookup"><span data-stu-id="e5f19-210">a.</span></span> <span data-ttu-id="e5f19-211">Щелкните **+ Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-211">Click **+User**.</span></span>
    
    <span data-ttu-id="e5f19-212">b.</span><span class="sxs-lookup"><span data-stu-id="e5f19-212">b.</span></span> <span data-ttu-id="e5f19-213">Введите соответствующие значения атрибутов учетной записи Azure AD в следующие текстовые поля: **Primary Email** (Основной электронный адрес), **Employee ID** (Идентификатор сотрудника), **Password** (Пароль), **Verify Password** (Проверка пароля), **Given Name** (Имя) и **Surname** (Фамилия).</span><span class="sxs-lookup"><span data-stu-id="e5f19-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="e5f19-214">c.</span><span class="sxs-lookup"><span data-stu-id="e5f19-214">c.</span></span> <span data-ttu-id="e5f19-215">Нажмите **Активный**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="e5f19-216">d.</span><span class="sxs-lookup"><span data-stu-id="e5f19-216">d.</span></span> <span data-ttu-id="e5f19-217">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e5f19-218">Вы можете использовать любые другие инструменты создания учетных записей пользователей SmarterU или API, предоставляемые SmarterU для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="e5f19-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e5f19-219">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5f19-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e5f19-220">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e5f19-222">**Чтобы назначить пользователя Britta Simon приложению SmarterU, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e5f19-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="e5f19-223">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e5f19-225">В списке приложений выберите **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-225">In the applications list, select **SmarterU**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="e5f19-227">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e5f19-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-229">Click **Add** button.</span></span> <span data-ttu-id="e5f19-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e5f19-232">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5f19-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5f19-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e5f19-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5f19-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e5f19-235">Testing single sign-on</span></span>

<span data-ttu-id="e5f19-236">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e5f19-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="e5f19-237">Щелкнув плитку SmarterU на панели доступа, вы автоматически войдете в приложение SmarterU.</span><span class="sxs-lookup"><span data-stu-id="e5f19-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="e5f19-238">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5f19-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="e5f19-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e5f19-239">Additional resources</span></span>

* [<span data-ttu-id="e5f19-240">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5f19-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5f19-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5f19-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

