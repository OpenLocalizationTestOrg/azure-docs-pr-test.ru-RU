---
title: "Учебник. Интеграция Azure Active Directory с Clarizen | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Clarizen."
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
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="92334-103">Руководство. Интеграция Azure Active Directory с Clarizen</span><span class="sxs-lookup"><span data-stu-id="92334-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="92334-104">В этом учебнике вы узнаете, как toointegrate Azure Active Directory (Azure AD) с Clarizen.</span><span class="sxs-lookup"><span data-stu-id="92334-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="92334-105">Это интеграция дает hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="92334-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="92334-106">Можно управлять, в Azure AD, кто имеет доступ tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="92334-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="92334-107">Вы можете включить вашей toobe пользователям автоматически входить в tooClarizen (единый вход) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92334-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="92334-108">Вы можете управлять учетными записями в одном централизованном месте hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="92334-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="92334-109">сценарий Hello в этом учебнике состоит из двух основных задач.</span><span class="sxs-lookup"><span data-stu-id="92334-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="92334-110">Добавление Clarizen из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="92334-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="92334-111">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92334-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="92334-112">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92334-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92334-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="92334-113">Prerequisites</span></span>
<span data-ttu-id="92334-114">tooconfigure интеграция Azure AD с Clarizen, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="92334-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="92334-115">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="92334-115">An Azure AD subscription</span></span>
- <span data-ttu-id="92334-116">подписка Clarizen с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="92334-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="92334-117">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="92334-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="92334-118">Проверьте единый вход Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="92334-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92334-119">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="92334-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="92334-120">Если у вас нет тестовой среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92334-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="92334-121">Добавление Clarizen из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="92334-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="92334-122">tooconfigure интеграция Clarizen hello в Azure AD, добавить Clarizen из hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="92334-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="92334-123">В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="92334-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Значок Azure Active Directory][1]

2. <span data-ttu-id="92334-125">Щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="92334-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="92334-126">Затем щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="92334-126">Then click **All applications**.</span></span>

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][2]

3. <span data-ttu-id="92334-128">Нажмите кнопку hello **добавить** кнопку вверху hello диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="92334-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![Кнопка «Добавить» Hello][3]

4. <span data-ttu-id="92334-130">Введите в поле поиска hello **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="92334-130">In hello search box, type **Clarizen**.</span></span>

    ![Введя «Clarizen» в поле поиска hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="92334-132">В области результатов hello, выберите **Clarizen**, а затем нажмите кнопку **добавить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="92334-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![При выборе Clarizen в области результатов hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="92334-134">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="92334-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="92334-135">В следующих разделах hello Настройка и тестирование Azure AD единого входа на основе пользовательского теста hello Саймон Britta Clarizen.</span><span class="sxs-lookup"><span data-stu-id="92334-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="92334-136">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Clarizen является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92334-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="92334-137">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Clarizen должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="92334-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="92334-138">Установления этой связи, назначив значение hello **имя пользователя** в Azure AD в качестве значения hello **Username** в Clarizen.</span><span class="sxs-lookup"><span data-stu-id="92334-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="92334-139">tooconfigure и теста Azure AD единого входа с Clarizen завершения hello следующие стандартные блоки:</span><span class="sxs-lookup"><span data-stu-id="92334-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="92334-140">**[Настройка Azure AD единого входа](#configure-azure-ad-single-sign-on)**  tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="92334-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92334-141">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="92334-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92334-142">**[Создание тестового пользователя Clarizen](#create-a-clarizen-test-user)**  toohave аналог Саймон Britta в Clarizen, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="92334-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="92334-143">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="92334-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92334-144">**[Тестирование единого входа](#test-single-sign-on)**  tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="92334-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="92334-145">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="92334-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="92334-146">Включите Azure AD единым входом в портал Azure hello и настройки единого входа в вашем приложении Clarizen.</span><span class="sxs-lookup"><span data-stu-id="92334-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="92334-147">В hello в hello портала Azure **Clarizen** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="92334-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Выбор пункта "Единый вход"][4]

2. <span data-ttu-id="92334-149">В hello **единого входа** диалоговом для **режим**выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="92334-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Выбор параметра "Единый вход на основе SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="92334-151">В hello **URL-адреса и домена Clarizen** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="92334-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Поля идентификатора и URL-адреса ответа](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="92334-153">а.</span><span class="sxs-lookup"><span data-stu-id="92334-153">a.</span></span> <span data-ttu-id="92334-154">В hello **идентификатор** поле типа значение hello в виде: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="92334-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="92334-155">b.</span><span class="sxs-lookup"><span data-stu-id="92334-155">b.</span></span> <span data-ttu-id="92334-156">В hello **URL-адрес ответа** введите URL-адрес, используя следующий шаблон hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="92334-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="92334-157">Они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="92334-157">These are not hello real values.</span></span> <span data-ttu-id="92334-158">Фактический идентификатор toouse hello и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="92334-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="92334-159">Здесь мы рекомендуем использовать hello уникальное значение строки, так как идентификатор hello.</span><span class="sxs-lookup"><span data-stu-id="92334-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="92334-160">фактические значения, обратитесь в службу hello hello tooget [Clarizen поддержки](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="92334-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="92334-161">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="92334-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Нажатие кнопки "Создать новый сертификат"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="92334-163">В hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите дату окончания действия.</span><span class="sxs-lookup"><span data-stu-id="92334-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="92334-164">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="92334-164">Then click **Save**.</span></span>

    ![Выбор и сохранение даты окончания действия](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="92334-166">В hello **сертификат подписи SAML** выберите **активировать новый сертификат**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="92334-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Установка флажка hello для создания нового сертификата hello active](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="92334-168">В hello **сертификат продолжения** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="92334-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Нажмите кнопку «ОК» tooconfirm требуется сертификат hello toomake active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="92334-170">В hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="92334-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Нажав кнопку загрузки hello toostart «Сертификат (Base64)»](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="92334-172">В hello **конфигурации Clarizen** щелкните **Настройка Clarizen** tooopen hello **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="92334-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Нажатие кнопки "Настроить Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Окно "Настройка единого входа" с файлами и URL-адресами](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="92334-175">В другом окне браузера Войдите на сайте компании tooyour Clarizen с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="92334-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="92334-176">Щелкните свое имя пользователя и выберите пункт **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="92334-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="92334-177">![Выбор пункта "Параметры" по именем пользователя](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="92334-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="92334-178">Нажмите кнопку hello **глобальные параметры** вкладки. Затем Далее слишком**федеративной проверки подлинности**, нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="92334-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="92334-179">![Вкладка "Глобальные параметры"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Глобальные параметры")</span><span class="sxs-lookup"><span data-stu-id="92334-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="92334-180">В hello **федеративной проверки подлинности** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="92334-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="92334-181">![Диалоговое окно "Федеративная проверка подлинности"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Федеративная проверка подлинности")</span><span class="sxs-lookup"><span data-stu-id="92334-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="92334-182">а.</span><span class="sxs-lookup"><span data-stu-id="92334-182">a.</span></span> <span data-ttu-id="92334-183">Выберите **Enable Federated Authentication** (Включить федеративную проверку подлинности).</span><span class="sxs-lookup"><span data-stu-id="92334-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="92334-184">b.</span><span class="sxs-lookup"><span data-stu-id="92334-184">b.</span></span> <span data-ttu-id="92334-185">Нажмите кнопку **отправить** tooupload загруженный сертификат.</span><span class="sxs-lookup"><span data-stu-id="92334-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="92334-186">c.</span><span class="sxs-lookup"><span data-stu-id="92334-186">c.</span></span> <span data-ttu-id="92334-187">В hello **URL-адрес входа** введите значение hello **SAML единого входа URL-адрес службы** из окна конфигурации приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92334-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="92334-188">d.</span><span class="sxs-lookup"><span data-stu-id="92334-188">d.</span></span> <span data-ttu-id="92334-189">В hello **URL-адрес выхода** введите значение hello **URL-адрес выхода** из окна конфигурации приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92334-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="92334-190">д.</span><span class="sxs-lookup"><span data-stu-id="92334-190">e.</span></span> <span data-ttu-id="92334-191">Установите флаг **Использовать POST**.</span><span class="sxs-lookup"><span data-stu-id="92334-191">Select **Use POST**.</span></span>

    <span data-ttu-id="92334-192">Е.</span><span class="sxs-lookup"><span data-stu-id="92334-192">f.</span></span> <span data-ttu-id="92334-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="92334-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="92334-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="92334-194">Create an Azure AD test user</span></span>
<span data-ttu-id="92334-195">В hello портал Azure Создание тестового пользователя вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="92334-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Имя и адрес электронной почты пользователя теста hello Azure AD][100]

1. <span data-ttu-id="92334-197">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="92334-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Значок Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="92334-199">Нажмите кнопку **пользователей и групп**, а затем нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="92334-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Выбор разделов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="92334-201">Вверху hello диалоговое окно «hello», нажмите кнопку **добавить** tooopen hello **пользователя** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="92334-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![Кнопка «Добавить» Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="92334-203">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="92334-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Диалоговое окно "Пользователь" с заполненными полями "Имя", "Адрес электронной почты" и "Пароль"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="92334-205">а.</span><span class="sxs-lookup"><span data-stu-id="92334-205">a.</span></span> <span data-ttu-id="92334-206">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92334-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92334-207">b.</span><span class="sxs-lookup"><span data-stu-id="92334-207">b.</span></span> <span data-ttu-id="92334-208">В hello **имя пользователя** поле введите адрес электронной почты hello hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="92334-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="92334-209">c.</span><span class="sxs-lookup"><span data-stu-id="92334-209">c.</span></span> <span data-ttu-id="92334-210">Выберите **Показать пароль** и запишите значение hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="92334-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="92334-211">d.</span><span class="sxs-lookup"><span data-stu-id="92334-211">d.</span></span> <span data-ttu-id="92334-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="92334-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="92334-213">Создание тестового пользователя Clarizen</span><span class="sxs-lookup"><span data-stu-id="92334-213">Create a Clarizen test user</span></span>
<span data-ttu-id="92334-214">tooenable toosign пользователей Azure AD в tooClarizen, необходимо подготовить учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="92334-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="92334-215">В случае hello объекта Clarizen Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="92334-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="92334-216">Войдите в tooyour Clarizen корпоративный сайт с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="92334-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="92334-217">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="92334-217">Click **People**.</span></span>

    <span data-ttu-id="92334-218">![Выберите пункт People (Пользователи)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="92334-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="92334-219">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="92334-219">Click **Invite User**.</span></span>

    <span data-ttu-id="92334-220">![Кнопка Invite User](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Пригласить пользователя")</span><span class="sxs-lookup"><span data-stu-id="92334-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="92334-221">В hello **пригласить пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="92334-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="92334-222">![Диалоговое окно Invite People](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="92334-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="92334-223">а.</span><span class="sxs-lookup"><span data-stu-id="92334-223">a.</span></span> <span data-ttu-id="92334-224">В hello **электронной почты** поле введите адрес электронной почты hello hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="92334-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="92334-225">b.</span><span class="sxs-lookup"><span data-stu-id="92334-225">b.</span></span> <span data-ttu-id="92334-226">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="92334-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92334-227">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="92334-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="92334-228">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="92334-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="92334-229">Включите toouse Britta Simon Azure единого входа путем предоставления ее tooClarizen доступа.</span><span class="sxs-lookup"><span data-stu-id="92334-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Назначение тестового пользователя][200]

1. <span data-ttu-id="92334-231">На hello портал Azure, откройте представление приложения hello, Обзор toohello представления каталога, **корпоративных приложений**, а затем нажмите кнопку **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="92334-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Выбор пунктов "Корпоративные приложения" и "Все приложения".][201]

2. <span data-ttu-id="92334-233">В списке приложений hello выберите **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="92334-233">In hello applications list, select **Clarizen**.</span></span>

    ![При выборе Clarizen в списке hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="92334-235">Hello левой панели щелкните **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="92334-235">In hello left pane, click **Users and groups**.</span></span>

    ![Выбор пункта "Пользователи и группы"][202]

4. <span data-ttu-id="92334-237">Нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="92334-237">Click hello **Add** button.</span></span> <span data-ttu-id="92334-238">Затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="92334-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Кнопка «Добавить» Hello и диалоговое окно «Добавление назначения» hello][203]

5. <span data-ttu-id="92334-240">В hello **пользователей и групп** выберите **Britta Simon** hello списка пользователей.</span><span class="sxs-lookup"><span data-stu-id="92334-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="92334-241">В hello **пользователей и групп** диалоговое окно, нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="92334-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="92334-242">В hello **добавить назначение** диалоговое окно, нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="92334-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="92334-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="92334-243">Test single sign-on</span></span>
<span data-ttu-id="92334-244">Тестирование конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="92334-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="92334-245">Если щелкнуть плитку Clarizen hello в hello панели доступа, вы должны автоматически входить в tooyour Clarizen приложения.</span><span class="sxs-lookup"><span data-stu-id="92334-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92334-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="92334-246">Additional resources</span></span>

* [<span data-ttu-id="92334-247">Список учебников по toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92334-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92334-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92334-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
