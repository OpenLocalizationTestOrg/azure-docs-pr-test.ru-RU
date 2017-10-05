---
title: "Учебник. Интеграция Azure Active Directory с Clarizen | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Clarizen."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="53796-103">Руководство. Интеграция Azure Active Directory с Clarizen</span><span class="sxs-lookup"><span data-stu-id="53796-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="53796-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="53796-105">Эта интеграция дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="53796-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="53796-106">С помощью Azure AD вы можете контролировать доступ к Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="53796-107">Вы можете включить автоматический вход пользователей в Clarizen (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="53796-108">Вы можете управлять учетными записями централизованно, через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="53796-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="53796-109">Сценарий, описанный в этом руководстве, состоит из двух основных задач.</span><span class="sxs-lookup"><span data-stu-id="53796-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="53796-110">Добавление Clarizen из коллекции.</span><span class="sxs-lookup"><span data-stu-id="53796-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="53796-111">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="53796-112">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53796-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53796-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="53796-113">Prerequisites</span></span>
<span data-ttu-id="53796-114">Чтобы настроить интеграцию Azure AD с Clarizen, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="53796-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="53796-115">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="53796-115">An Azure AD subscription</span></span>
- <span data-ttu-id="53796-116">подписка Clarizen с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="53796-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="53796-117">При проверке действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="53796-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="53796-118">Проверьте единый вход Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="53796-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53796-119">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="53796-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="53796-120">Если у вас нет тестовой среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53796-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="53796-121">Добавление Clarizen из коллекции</span><span class="sxs-lookup"><span data-stu-id="53796-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="53796-122">Чтобы настроить интеграцию Clarizen с Azure AD, добавьте Clarizen из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="53796-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="53796-123">На [портале Azure](https://portal.azure.com) в области слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53796-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Значок Azure Active Directory][1]

2. <span data-ttu-id="53796-125">Щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="53796-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="53796-126">Затем щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="53796-126">Then click **All applications**.</span></span>

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][2]

3. <span data-ttu-id="53796-128">В верхней части диалогового окна нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="53796-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![Кнопка "Добавить"][3]

4. <span data-ttu-id="53796-130">В поле поиска введите **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="53796-130">In the search box, type **Clarizen**.</span></span>

    ![Ввод Clarizen в поле поиска](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="53796-132">В области результатов выберите **Clarizen** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="53796-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Выбор Clarizen в области результатов](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="53796-134">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="53796-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="53796-135">В следующих разделах описана настройка и проверка единого входа Azure AD в Clarizen с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53796-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="53796-136">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Clarizen соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="53796-137">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="53796-138">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="53796-139">Чтобы настроить и проверить единый вход Azure AD в Clarizen, выполните инструкции ниже.</span><span class="sxs-lookup"><span data-stu-id="53796-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="53796-140">**[Настройте единый вход в Azure AD](#configure-azure-ad-single-sign-on)**, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="53796-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="53796-141">**[Создайте тестового пользователя Azure AD](#create-an-azure-ad-test-user)** для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53796-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53796-142">**[Создайте тестового пользователя Clarizen](#create-a-clarizen-test-user)**, чтобы в Clarizen был тестовый пользователь Britta Simon, связанный с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="53796-143">**[Назначьте тестового пользователя Azure AD](#assign-the-azure-ad-test-user)**, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53796-144">**[Проверьте единый вход](#test-single-sign-on)**, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="53796-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="53796-145">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="53796-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="53796-146">Включите единый вход Azure AD на портале Azure и настройте его в приложении Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="53796-147">На портале Azure на странице интеграции с приложением **Clarizen** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="53796-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Выбор пункта "Единый вход"][4]

2. <span data-ttu-id="53796-149">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="53796-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Выбор параметра "Единый вход на основе SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="53796-151">В разделе **Домены и URL-адреса приложения Clarizen** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="53796-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Поля идентификатора и URL-адреса ответа](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="53796-153">а.</span><span class="sxs-lookup"><span data-stu-id="53796-153">a.</span></span> <span data-ttu-id="53796-154">В поле **Идентификатор** введите значение **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="53796-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="53796-155">b.</span><span class="sxs-lookup"><span data-stu-id="53796-155">b.</span></span> <span data-ttu-id="53796-156">В поле **URL-адрес ответа** введите URL-адрес, используя следующий шаблон: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="53796-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="53796-157">Значения, указанные выше, приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="53796-157">These are not the real values.</span></span> <span data-ttu-id="53796-158">Используйте фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="53796-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="53796-159">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="53796-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="53796-160">Чтобы получить фактические значения, обратитесь в [техническую поддержку Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="53796-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="53796-161">В разделе **Сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="53796-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Нажатие кнопки "Создать новый сертификат"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="53796-163">В диалоговом окне **Создание нового сертификата** щелкните значок календаря и выберите дату окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="53796-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="53796-164">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="53796-164">Then click **Save**.</span></span>

    ![Выбор и сохранение даты окончания действия](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="53796-166">В разделе **Сертификат подписи SAML** поставьте флажок **Сделать новый сертификат активным** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="53796-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Установка флажка для активации нового сертификата](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="53796-168">В диалоговом окне **Сертификат возобновления** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="53796-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Нажатие кнопки "ОК" для подтверждения активации сертификата](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="53796-170">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="53796-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Нажатие кнопки "Сертификат (Base64)" для начала загрузки](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="53796-172">В разделе **Конфигурация Clarizen** нажмите кнопку **Настроить Clarizen**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="53796-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Нажатие кнопки "Настроить Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Окно "Настройка единого входа" с файлами и URL-адресами](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="53796-175">В другом окне веб-браузера войдите на корпоративный сайт Clarizen в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="53796-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="53796-176">Щелкните свое имя пользователя и выберите пункт **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="53796-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="53796-177">![Выбор пункта "Параметры" по именем пользователя](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="53796-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="53796-178">Откройте вкладку **Global Settings** (Глобальные параметры).</span><span class="sxs-lookup"><span data-stu-id="53796-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="53796-179">Рядом с параметром **Federated Authentication** (Федеративная проверка подлинности) нажмите кнопку **edit** (изменить).</span><span class="sxs-lookup"><span data-stu-id="53796-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="53796-180">![Вкладка "Глобальные параметры"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Глобальные параметры")</span><span class="sxs-lookup"><span data-stu-id="53796-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="53796-181">В диалоговом окне **Federated Authentication** (Федеративная проверка подлинности) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="53796-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="53796-182">![Диалоговое окно "Федеративная проверка подлинности"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Федеративная проверка подлинности")</span><span class="sxs-lookup"><span data-stu-id="53796-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="53796-183">а.</span><span class="sxs-lookup"><span data-stu-id="53796-183">a.</span></span> <span data-ttu-id="53796-184">Выберите **Enable Federated Authentication** (Включить федеративную проверку подлинности).</span><span class="sxs-lookup"><span data-stu-id="53796-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="53796-185">b.</span><span class="sxs-lookup"><span data-stu-id="53796-185">b.</span></span> <span data-ttu-id="53796-186">Чтобы отправить загруженный сертификат, нажмите кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="53796-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="53796-187">c.</span><span class="sxs-lookup"><span data-stu-id="53796-187">c.</span></span> <span data-ttu-id="53796-188">В текстовом поле **Sign-in URL** (URL-адрес входа) введите значение **URL-адреса службы единого входа SAML** из окна настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="53796-189">d.</span><span class="sxs-lookup"><span data-stu-id="53796-189">d.</span></span> <span data-ttu-id="53796-190">В текстовом поле **Sign-out URL** (URL-адрес выхода) введите значение **URL-адреса выхода** из окна настройки приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53796-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="53796-191">д.</span><span class="sxs-lookup"><span data-stu-id="53796-191">e.</span></span> <span data-ttu-id="53796-192">Установите флаг **Использовать POST**.</span><span class="sxs-lookup"><span data-stu-id="53796-192">Select **Use POST**.</span></span>

    <span data-ttu-id="53796-193">Е.</span><span class="sxs-lookup"><span data-stu-id="53796-193">f.</span></span> <span data-ttu-id="53796-194">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="53796-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="53796-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="53796-195">Create an Azure AD test user</span></span>
<span data-ttu-id="53796-196">На портале Azure создайте тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53796-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Имя и адрес электронной почты тестового пользователя Azure AD][100]

1. <span data-ttu-id="53796-198">На портале Azure в области слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53796-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Значок Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="53796-200">Откройте раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="53796-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Выбор разделов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="53796-202">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="53796-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="53796-204">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="53796-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь" с заполненными полями "Имя", "Адрес электронной почты" и "Пароль"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="53796-206">а.</span><span class="sxs-lookup"><span data-stu-id="53796-206">a.</span></span> <span data-ttu-id="53796-207">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53796-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53796-208">b.</span><span class="sxs-lookup"><span data-stu-id="53796-208">b.</span></span> <span data-ttu-id="53796-209">В поле **Имя пользователя** введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53796-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="53796-210">c.</span><span class="sxs-lookup"><span data-stu-id="53796-210">c.</span></span> <span data-ttu-id="53796-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="53796-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="53796-212">d.</span><span class="sxs-lookup"><span data-stu-id="53796-212">d.</span></span> <span data-ttu-id="53796-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="53796-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="53796-214">Создание тестового пользователя Clarizen</span><span class="sxs-lookup"><span data-stu-id="53796-214">Create a Clarizen test user</span></span>
<span data-ttu-id="53796-215">Чтобы пользователи Azure AD могли входить в приложение Clarizen, необходимо подготовить учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="53796-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="53796-216">В случае с Clarizen подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="53796-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="53796-217">Войдите на корпоративный сайт Clarizen в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="53796-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="53796-218">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="53796-218">Click **People**.</span></span>

    <span data-ttu-id="53796-219">![Выберите пункт People (Пользователи)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="53796-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="53796-220">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="53796-220">Click **Invite User**.</span></span>

    <span data-ttu-id="53796-221">![Кнопка Invite User](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Пригласить пользователя")</span><span class="sxs-lookup"><span data-stu-id="53796-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="53796-222">В диалоговом окне **Invite People** (Приглашение пользователей) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="53796-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="53796-223">![Диалоговое окно Invite People](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="53796-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="53796-224">а.</span><span class="sxs-lookup"><span data-stu-id="53796-224">a.</span></span> <span data-ttu-id="53796-225">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53796-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="53796-226">b.</span><span class="sxs-lookup"><span data-stu-id="53796-226">b.</span></span> <span data-ttu-id="53796-227">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="53796-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53796-228">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="53796-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="53796-229">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="53796-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="53796-230">Разрешите пользователю Britta Simon применять единый вход Azure, предоставив доступ к Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Назначение тестового пользователя][200]

1. <span data-ttu-id="53796-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="53796-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][201]

2. <span data-ttu-id="53796-234">В списке приложений выберите **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="53796-234">In the applications list, select **Clarizen**.</span></span>

    ![Выбор Clarizen в списке](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="53796-236">В области слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="53796-236">In the left pane, click **Users and groups**.</span></span>

    ![Выбор пункта "Пользователи и группы"][202]

4. <span data-ttu-id="53796-238">Нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="53796-238">Click the **Add** button.</span></span> <span data-ttu-id="53796-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="53796-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Нажатие кнопки "Добавить" и диалоговое окно "Добавление назначения"][203]

5. <span data-ttu-id="53796-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="53796-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="53796-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="53796-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="53796-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="53796-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="53796-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="53796-244">Test single sign-on</span></span>
<span data-ttu-id="53796-245">Проверьте конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="53796-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="53796-246">Щелкнув элемент Clarizen на панели доступа, вы автоматически войдете в приложение Clarizen.</span><span class="sxs-lookup"><span data-stu-id="53796-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53796-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="53796-247">Additional resources</span></span>

* [<span data-ttu-id="53796-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53796-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53796-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="53796-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
