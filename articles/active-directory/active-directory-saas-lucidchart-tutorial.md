---
title: "Учебник. Интеграция Azure Active Directory с Lucidchart | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Lucidchart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="29307-103">Руководство. Интеграция Azure Active Directory с Lucidchart</span><span class="sxs-lookup"><span data-stu-id="29307-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="29307-104">В этом руководстве описано, как интегрировать Lucidchart с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29307-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29307-105">Интеграция Azure AD с приложением Lucidchart обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="29307-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29307-106">С помощью Azure AD можно управлять доступом к Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="29307-107">Вы можете включить автоматический вход пользователей в Lucidchart (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29307-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29307-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="29307-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="29307-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29307-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29307-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="29307-110">Prerequisites</span></span>

<span data-ttu-id="29307-111">Чтобы настроить интеграцию Azure AD с приложением Lucidchart, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="29307-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="29307-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="29307-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29307-113">Подписка с поддержкой единого входа Lucidchart</span><span class="sxs-lookup"><span data-stu-id="29307-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29307-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="29307-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29307-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="29307-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29307-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="29307-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29307-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29307-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29307-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="29307-118">Scenario description</span></span>
<span data-ttu-id="29307-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="29307-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29307-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="29307-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29307-121">Добавление Lucidchart из коллекции</span><span class="sxs-lookup"><span data-stu-id="29307-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="29307-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29307-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="29307-123">Добавление Lucidchart из коллекции</span><span class="sxs-lookup"><span data-stu-id="29307-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="29307-124">Чтобы настроить интеграцию Lucidchart с Azure AD, необходимо добавить Lucidchart из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="29307-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29307-125">**Чтобы добавить Lucidchart из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="29307-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29307-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29307-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29307-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="29307-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29307-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29307-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="29307-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="29307-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="29307-133">В поле поиска введите **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="29307-133">In the search box, type **Lucidchart**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="29307-135">На панели результатов выберите **Lucidchart**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="29307-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29307-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29307-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29307-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lucidchart с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29307-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29307-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Lucidchart соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29307-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="29307-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="29307-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29307-142">Чтобы настроить и проверить единый вход Azure AD в Lucidchart, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="29307-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29307-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="29307-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29307-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29307-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29307-145">**[Создание тестового пользователя Lucidchart](#creating-a-lucidchart-test-user)** требуется для создания в Lucidchart пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29307-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29307-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29307-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29307-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="29307-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29307-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29307-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29307-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="29307-150">**Чтобы настроить единый вход Azure AD в Lucidchart, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="29307-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="29307-151">На портале Azure на странице интеграции с приложением **Lucidchart** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="29307-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="29307-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="29307-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="29307-155">В разделе **Домен и URL-адреса приложения Lucidchart** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29307-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="29307-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://chart2.office.lucidchart.com/saml/sso/azure`.</span><span class="sxs-lookup"><span data-stu-id="29307-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="29307-158">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="29307-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="29307-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="29307-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29307-162">В другом окне веб-браузера зайдите на веб-сайт компании Lucidchart в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="29307-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="29307-163">В верхнем меню нажмите пункт **Группа**.</span><span class="sxs-lookup"><span data-stu-id="29307-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="29307-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team") (Команда)</span><span class="sxs-lookup"><span data-stu-id="29307-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="29307-165">Выберите **Приложение \> Управление SAML**.</span><span class="sxs-lookup"><span data-stu-id="29307-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="29307-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML") (Управление SAML)</span><span class="sxs-lookup"><span data-stu-id="29307-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="29307-167">На странице диалогового окна **Параметры проверки подлинности SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29307-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="29307-168">а.</span><span class="sxs-lookup"><span data-stu-id="29307-168">a.</span></span> <span data-ttu-id="29307-169">Установите флажок **Enable SAML Authentication** (Включить аутентификацию SAML), а затем выберите **Optional** (Необязательно).</span><span class="sxs-lookup"><span data-stu-id="29307-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="29307-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings") (Параметры аутентификации SAML)</span><span class="sxs-lookup"><span data-stu-id="29307-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="29307-171">b.</span><span class="sxs-lookup"><span data-stu-id="29307-171">b.</span></span> <span data-ttu-id="29307-172">В текстовом поле **Domain** (Домен) введите свой домен и нажмите кнопку **Change Certificate** (Изменить сертификат).</span><span class="sxs-lookup"><span data-stu-id="29307-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="29307-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate") (Изменить сертификат)</span><span class="sxs-lookup"><span data-stu-id="29307-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="29307-174">c.</span><span class="sxs-lookup"><span data-stu-id="29307-174">c.</span></span> <span data-ttu-id="29307-175">Откройте скачанный файл метаданных, скопируйте его содержимое и вставьте его в текстовое поле **Отправка метаданных** .</span><span class="sxs-lookup"><span data-stu-id="29307-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="29307-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata") (Передача метаданных)</span><span class="sxs-lookup"><span data-stu-id="29307-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="29307-177">г)</span><span class="sxs-lookup"><span data-stu-id="29307-177">d.</span></span> <span data-ttu-id="29307-178">Установите флажок **Автоматически добавлять новых пользователей в группу**, а затем нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="29307-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="29307-179">![Сохранение изменений](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Сохранение изменений")</span><span class="sxs-lookup"><span data-stu-id="29307-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="29307-180">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="29307-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29307-181">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="29307-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29307-182">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="29307-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29307-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29307-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="29307-184">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29307-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="29307-186">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="29307-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29307-187">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29307-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29307-189">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="29307-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29307-191">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29307-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29307-193">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="29307-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29307-195">а.</span><span class="sxs-lookup"><span data-stu-id="29307-195">a.</span></span> <span data-ttu-id="29307-196">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29307-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29307-197">b.</span><span class="sxs-lookup"><span data-stu-id="29307-197">b.</span></span> <span data-ttu-id="29307-198">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29307-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29307-199">c.</span><span class="sxs-lookup"><span data-stu-id="29307-199">c.</span></span> <span data-ttu-id="29307-200">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="29307-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="29307-201">d.</span><span class="sxs-lookup"><span data-stu-id="29307-201">d.</span></span> <span data-ttu-id="29307-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29307-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="29307-203">Создание тестового пользователя Lucidchart</span><span class="sxs-lookup"><span data-stu-id="29307-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="29307-204">Элемент действия для настройки подготовки пользователей в Lucidchart отсутствует.</span><span class="sxs-lookup"><span data-stu-id="29307-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="29307-205">Когда назначенный пользователь пытается войти в Lucidchart с помощью панели доступа, Lucidchart проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="29307-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="29307-206">Если учетная запись пользователя отсутствует, Lucidchart автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="29307-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="29307-207">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29307-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="29307-208">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="29307-210">**Чтобы назначить пользователя Britta Simon в Lucidchart, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="29307-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="29307-211">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29307-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="29307-213">В списке приложений выберите **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="29307-213">In the applications list, select **Lucidchart**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="29307-215">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29307-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="29307-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29307-217">Click **Add** button.</span></span> <span data-ttu-id="29307-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29307-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="29307-220">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29307-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29307-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="29307-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29307-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="29307-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29307-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="29307-223">Testing single sign-on</span></span>

<span data-ttu-id="29307-224">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="29307-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29307-225">Щелкнув плитку Lucidchart на панели доступа, вы автоматически войдете в приложение Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="29307-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="29307-226">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29307-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29307-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="29307-227">Additional resources</span></span>

* [<span data-ttu-id="29307-228">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29307-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29307-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29307-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

