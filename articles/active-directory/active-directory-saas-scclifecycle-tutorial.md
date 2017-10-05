---
title: "Руководство по интеграции Azure Active Directory с SCC LifeCycle | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0f8f9d03e8c35109b74088350ef1d68f6b823e8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="f62ff-103">Учебник. Интеграция Azure Active Directory с SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="f62ff-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="f62ff-104">В этом руководстве описано, как интегрировать SCC LifeCycle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f62ff-104">In this tutorial, you learn how to integrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f62ff-105">Интеграция Azure AD с приложением SCC LifeCycle обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f62ff-105">Integrating SCC LifeCycle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f62ff-106">С помощью Azure AD вы можете контролировать доступ к SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-106">You can control in Azure AD who has access to SCC LifeCycle</span></span>
- <span data-ttu-id="f62ff-107">Вы можете включить автоматический вход пользователей в SCC LifeCycle (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f62ff-107">You can enable your users to automatically get signed-on to SCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f62ff-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f62ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f62ff-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f62ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f62ff-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f62ff-110">Prerequisites</span></span>

<span data-ttu-id="f62ff-111">Чтобы настроить интеграцию Azure AD с SCC LifeCycle, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f62ff-111">To configure Azure AD integration with SCC LifeCycle, you need the following items:</span></span>

- <span data-ttu-id="f62ff-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f62ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f62ff-113">подписка SCC LifeCycle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f62ff-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f62ff-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f62ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f62ff-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f62ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f62ff-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f62ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f62ff-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f62ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f62ff-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f62ff-118">Scenario description</span></span>
<span data-ttu-id="f62ff-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f62ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f62ff-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f62ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f62ff-121">Добавление SCC LifeCycle из коллекции.</span><span class="sxs-lookup"><span data-stu-id="f62ff-121">Adding SCC LifeCycle from the gallery</span></span>
2. <span data-ttu-id="f62ff-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f62ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-the-gallery"></a><span data-ttu-id="f62ff-123">Добавление SCC LifeCycle из коллекции</span><span class="sxs-lookup"><span data-stu-id="f62ff-123">Adding SCC LifeCycle from the gallery</span></span>
<span data-ttu-id="f62ff-124">Чтобы настроить интеграцию SCC LifeCycle с Azure AD, необходимо добавить SCC LifeCycle из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f62ff-124">To configure the integration of SCC LifeCycle into Azure AD, you need to add SCC LifeCycle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f62ff-125">**Чтобы добавить SCC LifeCycle из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f62ff-125">**To add SCC LifeCycle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f62ff-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f62ff-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f62ff-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f62ff-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f62ff-133">В поле поиска введите **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-133">In the search box, type **SCC LifeCycle**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="f62ff-135">На панели результатов выберите **SCC LifeCycle** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="f62ff-135">In the results panel, select **SCC LifeCycle**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f62ff-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f62ff-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f62ff-138">В этом разделе описана настройка и проверка единого входа Azure AD в SCC LifeCycle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f62ff-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f62ff-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в SCC LifeCycle соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f62ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SCC LifeCycle is to a user in Azure AD.</span></span> <span data-ttu-id="f62ff-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-140">In other words, a link relationship between an Azure AD user and the related user in SCC LifeCycle needs to be established.</span></span>

<span data-ttu-id="f62ff-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-141">In SCC LifeCycle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f62ff-142">Чтобы настроить и проверить единый вход Azure AD в SCC LifeCycle, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="f62ff-142">To configure and test Azure AD single sign-on with SCC LifeCycle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f62ff-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f62ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f62ff-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f62ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f62ff-145">**[Создание тестового пользователя SCC LifeCycle](#creating-an-scc-lifecycle-test-user)** требуется для того, чтобы в SCC LifeCycle существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f62ff-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - to have a counterpart of Britta Simon in SCC LifeCycle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f62ff-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f62ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f62ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f62ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f62ff-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f62ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f62ff-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="f62ff-150">**Чтобы настроить единый вход Azure AD в SCC LifeCycle, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f62ff-150">**To configure Azure AD single sign-on with SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="f62ff-151">На портале Azure на странице интеграции с приложением **SCC LifeCycle** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-151">In the Azure portal, on the **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f62ff-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f62ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="f62ff-155">В разделе **Домены и URL-адреса приложения SCC LifeCycle** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f62ff-155">On the **SCC LifeCycle Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="f62ff-157">а.</span><span class="sxs-lookup"><span data-stu-id="f62ff-157">a.</span></span> <span data-ttu-id="f62ff-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="f62ff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="f62ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="f62ff-159">b.</span></span> <span data-ttu-id="f62ff-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f62ff-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="f62ff-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f62ff-161">These values are not real.</span></span> <span data-ttu-id="f62ff-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="f62ff-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f62ff-163">Чтобы получить их, обратитесь к [группе поддержки клиентов SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="f62ff-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f62ff-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f62ff-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="f62ff-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f62ff-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f62ff-168">Чтобы настроить единый вход на стороне **SCC LifeCycle**, отправьте скачанный **XML-файл метаданных** [группе поддержки SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="f62ff-168">To configure single sign-on on **SCC LifeCycle** side, you need to send the downloaded **Metadata XML** to [SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="f62ff-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="f62ff-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="f62ff-170">Единый вход должна включить группа поддержки SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-170">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="f62ff-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f62ff-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f62ff-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f62ff-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f62ff-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f62ff-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f62ff-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f62ff-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="f62ff-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f62ff-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f62ff-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f62ff-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f62ff-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f62ff-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f62ff-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f62ff-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f62ff-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f62ff-186">а.</span><span class="sxs-lookup"><span data-stu-id="f62ff-186">a.</span></span> <span data-ttu-id="f62ff-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f62ff-188">b.</span><span class="sxs-lookup"><span data-stu-id="f62ff-188">b.</span></span> <span data-ttu-id="f62ff-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f62ff-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f62ff-190">c.</span><span class="sxs-lookup"><span data-stu-id="f62ff-190">c.</span></span> <span data-ttu-id="f62ff-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f62ff-192">d.</span><span class="sxs-lookup"><span data-stu-id="f62ff-192">d.</span></span> <span data-ttu-id="f62ff-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="f62ff-194">Создание тестового пользователя SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="f62ff-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="f62ff-195">Чтобы пользователи Azure AD могли выполнять вход в SCC LifeCycle, они должны быть подготовлены для SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-195">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="f62ff-196">Действие для настройки подготовки пользователей в SCC LifeCycle отсутствует.</span><span class="sxs-lookup"><span data-stu-id="f62ff-196">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="f62ff-197">Когда назначенный пользователь пытается войти в SCC LifeCycle, учетная запись SCC LifeCycle создается автоматически (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="f62ff-197">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="f62ff-198">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f62ff-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f62ff-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f62ff-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f62ff-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SCC LifeCycle.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f62ff-202">**Чтобы назначить пользователя Britta Simon в SCC LifeCycle, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f62ff-202">**To assign Britta Simon to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="f62ff-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications.**</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f62ff-205">Из списка приложений выберите **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-205">In the applications list, select **SCC LifeCycle**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="f62ff-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f62ff-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-209">Click **Add** button.</span></span> <span data-ttu-id="f62ff-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f62ff-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f62ff-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f62ff-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f62ff-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f62ff-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f62ff-215">Testing single sign-on</span></span>

<span data-ttu-id="f62ff-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f62ff-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f62ff-217">Щелкнув элемент "SCC LifeCycle" на панели доступа, вы автоматически войдете в приложение SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="f62ff-217">When you click the SCC LifeCycle tile in the Access Panel, you should get automatically signed-on to SCC LifeCycle application.</span></span>
<span data-ttu-id="f62ff-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f62ff-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f62ff-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f62ff-219">Additional resources</span></span>

* [<span data-ttu-id="f62ff-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f62ff-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f62ff-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f62ff-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png

