---
title: "Руководство по интеграции Azure Active Directory с Atomic Learning | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложение Atomic Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 6cce8fc839e60eb6498ab48bf68e9906c98889a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="5c02e-103">Руководство. Интеграция Azure Active Directory с Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="5c02e-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="5c02e-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c02e-105">Интеграция приложения Atomic Learning с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5c02e-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c02e-106">С помощью Azure AD вы можете контролировать доступ к Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-106">You can control in Azure AD who has access to Atomic Learning</span></span>
- <span data-ttu-id="5c02e-107">Вы можете включить автоматический вход пользователей в Atomic Learning (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c02e-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c02e-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5c02e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c02e-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c02e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c02e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c02e-110">Prerequisites</span></span>

<span data-ttu-id="5c02e-111">Чтобы настроить интеграцию Azure AD с Atomic Learning, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5c02e-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

- <span data-ttu-id="5c02e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5c02e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c02e-113">подписка Atomic Learning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c02e-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c02e-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5c02e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c02e-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5c02e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c02e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5c02e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c02e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c02e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c02e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5c02e-118">Scenario description</span></span>
<span data-ttu-id="5c02e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5c02e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c02e-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5c02e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c02e-121">Добавление Atomic Learning из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c02e-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="5c02e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c02e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="5c02e-123">Добавление Atomic Learning из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c02e-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="5c02e-124">Чтобы настроить интеграцию Atomic Learning с Azure AD, необходимо добавить Atomic Learning из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c02e-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c02e-125">**Чтобы добавить Atomic Learning из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c02e-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c02e-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c02e-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c02e-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5c02e-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5c02e-133">В поле поиска введите **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-133">In the search box, type **Atomic Learning**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="5c02e-135">На панели результатов выберите **Atomic Learning** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="5c02e-135">In the results panel, select **Atomic Learning**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c02e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c02e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c02e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Atomic Learning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c02e-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c02e-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Atomic Learning соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c02e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="5c02e-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-140">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>

<span data-ttu-id="5c02e-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-141">In Atomic Learning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c02e-142">Чтобы настроить и проверить единый вход Azure AD в Atomic Learning, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5c02e-142">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c02e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5c02e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c02e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c02e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c02e-145">**[Создание тестового пользователя Atomic Learning](#creating-an-atomic-learning-test-user)** нужно для того, чтобы в Atomic Learning также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c02e-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c02e-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c02e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c02e-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5c02e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c02e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c02e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c02e-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="5c02e-150">**Чтобы настроить единый вход Azure AD в Atomic Learning, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c02e-150">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="5c02e-151">На портале Azure на странице интеграции с приложением **Atomic Learning** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-151">In the Azure portal, on the **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5c02e-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c02e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="5c02e-155">В разделе **Домены и URL-адреса приложения Atomic Learning** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c02e-155">On the **Atomic Learning Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="5c02e-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5c02e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="5c02e-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="5c02e-158">This value is not real.</span></span> <span data-ttu-id="5c02e-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="5c02e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5c02e-160">Для получения этого значения обратитесь к [группе поддержки Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="5c02e-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) to get this value.</span></span> 
 
4. <span data-ttu-id="5c02e-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c02e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="5c02e-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5c02e-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c02e-165">Чтобы настроить единый вход на стороне **Atomic Learning**, отправьте скачанный **XML-файл метаданных** [группе поддержки Atomic Learning](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="5c02e-165">To configure single sign-on on **Atomic Learning** side, you need to send the downloaded **Metadata XML** to [Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="5c02e-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="5c02e-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5c02e-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5c02e-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c02e-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5c02e-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c02e-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5c02e-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c02e-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c02e-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c02e-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c02e-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5c02e-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c02e-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c02e-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c02e-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c02e-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c02e-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c02e-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c02e-182">а.</span><span class="sxs-lookup"><span data-stu-id="5c02e-182">a.</span></span> <span data-ttu-id="5c02e-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c02e-184">b.</span><span class="sxs-lookup"><span data-stu-id="5c02e-184">b.</span></span> <span data-ttu-id="5c02e-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c02e-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c02e-186">c.</span><span class="sxs-lookup"><span data-stu-id="5c02e-186">c.</span></span> <span data-ttu-id="5c02e-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c02e-188">d.</span><span class="sxs-lookup"><span data-stu-id="5c02e-188">d.</span></span> <span data-ttu-id="5c02e-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="5c02e-190">Создание тестового пользователя Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="5c02e-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="5c02e-191">В этом разделе описано, как создать пользователя Britta Simon в приложении Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="5c02e-192">Приложение Atomic Learning поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5c02e-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="5c02e-193">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="5c02e-193">There is no action item for you in this section.</span></span> <span data-ttu-id="5c02e-194">Пользователь будет создан при попытке получить доступ к приложению Atomic Learning (если он еще не создан). Для этого будет использоваться адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5c02e-194">A new user is created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c02e-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c02e-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c02e-196">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atomic Learning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5c02e-198">**Чтобы назначить пользователя Britta Simon в Atomic Learning, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c02e-198">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="5c02e-199">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5c02e-201">В списке приложений выберите **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-201">In the applications list, select **Atomic Learning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="5c02e-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5c02e-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-205">Click **Add** button.</span></span> <span data-ttu-id="5c02e-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5c02e-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c02e-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c02e-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5c02e-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c02e-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5c02e-211">Testing single sign-on</span></span>

<span data-ttu-id="5c02e-212">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5c02e-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c02e-213">Щелкнув плитку Atomic Learning на панели доступа, вы автоматически войдете в приложение Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="5c02e-213">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>
<span data-ttu-id="5c02e-214">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c02e-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c02e-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5c02e-215">Additional resources</span></span>

* [<span data-ttu-id="5c02e-216">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c02e-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c02e-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c02e-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

