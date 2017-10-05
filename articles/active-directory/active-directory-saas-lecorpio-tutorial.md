---
title: "Руководство по интеграции Azure Active Directory с Lecorpio | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="44484-103">Руководство. Интеграция Azure Active Directory с Lecorpio</span><span class="sxs-lookup"><span data-stu-id="44484-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="44484-104">Из этого руководства вы узнаете, как интегрировать Lecorpio с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44484-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44484-105">Интеграция Lecorpio с Azure AD позволяет получить следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="44484-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44484-106">С помощью Azure AD вы можете контролировать доступ к Lecorpio</span><span class="sxs-lookup"><span data-stu-id="44484-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="44484-107">Вы можете включить автоматический вход пользователей в Lecorpio (единый вход) с учетной записью Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44484-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="44484-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44484-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44484-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44484-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44484-110">Prerequisites</span></span>

<span data-ttu-id="44484-111">Чтобы настроить интеграцию Azure AD с Lecorpio, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="44484-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="44484-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="44484-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44484-113">подписка Lecorpio с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="44484-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44484-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="44484-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44484-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="44484-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44484-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="44484-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44484-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44484-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44484-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="44484-118">Scenario description</span></span>
<span data-ttu-id="44484-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44484-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44484-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="44484-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44484-121">Добавление Lecorpio из коллекции</span><span class="sxs-lookup"><span data-stu-id="44484-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="44484-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="44484-123">Добавление Lecorpio из коллекции</span><span class="sxs-lookup"><span data-stu-id="44484-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="44484-124">Чтобы настроить интеграцию Lecorpio с Azure AD, необходимо добавить Lecorpio из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="44484-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44484-125">**Чтобы добавить Lecorpio из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44484-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44484-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44484-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44484-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="44484-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44484-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44484-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="44484-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="44484-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="44484-133">В поле поиска введите **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="44484-133">In the search box, type **Lecorpio**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="44484-135">На панели результатов выберите **Lecorpio**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="44484-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44484-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44484-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в Lecorpio с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44484-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44484-139">Для настройки единого входа в Azure AD необходимо знать, какой пользователь в Lecorpio соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44484-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="44484-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="44484-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="44484-142">Чтобы настроить и проверить единый вход Azure AD в Lecorpio, необходимо выполнить следующие стандартные действия:</span><span class="sxs-lookup"><span data-stu-id="44484-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44484-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="44484-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44484-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44484-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44484-145">**[Создание тестового пользователя Lecorpio](#creating-a-lecorpio-test-user)** требуется для создания в Lecorpio пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44484-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44484-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44484-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44484-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="44484-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44484-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44484-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и как настроить его в приложении Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="44484-150">**Чтобы настроить единый вход Azure AD в Lecorpio, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44484-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="44484-151">На портале Azure на странице интеграции с приложением **Lecorpio** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="44484-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="44484-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="44484-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="44484-155">В разделе **Домены и URL-адреса приложения Lecorpio** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="44484-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="44484-157">а.</span><span class="sxs-lookup"><span data-stu-id="44484-157">a.</span></span> <span data-ttu-id="44484-158">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<instance name>.lecorpio.com/<customer name>`.</span><span class="sxs-lookup"><span data-stu-id="44484-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="44484-159">b.</span><span class="sxs-lookup"><span data-stu-id="44484-159">b.</span></span> <span data-ttu-id="44484-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="44484-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44484-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="44484-161">These values are not the real.</span></span> <span data-ttu-id="44484-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="44484-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="44484-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="44484-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="44484-164">Чтобы получить их, обратитесь в [службу поддержки клиентов Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="44484-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="44484-165">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="44484-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="44484-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="44484-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44484-169">Чтобы настроить единый вход на стороне **Lecorpio**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="44484-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="44484-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="44484-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44484-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="44484-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44484-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="44484-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44484-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="44484-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44484-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="44484-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44484-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44484-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44484-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44484-179">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="44484-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44484-181">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="44484-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44484-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="44484-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44484-185">а.</span><span class="sxs-lookup"><span data-stu-id="44484-185">a.</span></span> <span data-ttu-id="44484-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44484-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44484-187">b.</span><span class="sxs-lookup"><span data-stu-id="44484-187">b.</span></span> <span data-ttu-id="44484-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44484-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44484-189">c.</span><span class="sxs-lookup"><span data-stu-id="44484-189">c.</span></span> <span data-ttu-id="44484-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="44484-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44484-191">d.</span><span class="sxs-lookup"><span data-stu-id="44484-191">d.</span></span> <span data-ttu-id="44484-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44484-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="44484-193">Создание тестового пользователя Lecorpio</span><span class="sxs-lookup"><span data-stu-id="44484-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="44484-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="44484-195">Чтобы добавить пользователей в приложение Lecorpio, обратитесь в [службу поддержки клиентов Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="44484-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44484-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44484-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44484-197">В этом разделе описано, как настроить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="44484-199">**Чтобы назначить пользователя Britta Simon для приложения Lecorpio, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44484-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="44484-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44484-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="44484-202">В списке приложений выберите **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="44484-202">In the applications list, select **Lecorpio**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="44484-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44484-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="44484-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44484-206">Click **Add** button.</span></span> <span data-ttu-id="44484-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44484-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="44484-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44484-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44484-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="44484-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44484-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="44484-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44484-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="44484-212">Testing single sign-on</span></span>

<span data-ttu-id="44484-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="44484-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44484-214">Щелкнув элемент Lecorpio на панели доступа, вы автоматически войдете в приложение Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="44484-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44484-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="44484-215">Additional resources</span></span>

* [<span data-ttu-id="44484-216">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44484-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44484-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44484-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

