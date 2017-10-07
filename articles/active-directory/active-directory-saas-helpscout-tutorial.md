---
title: "Учебник. Интеграция Azure Active Directory с Help Scout | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и помочь Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="ddc55-103">Учебник. Интеграция Azure Active Directory с Help Scout</span><span class="sxs-lookup"><span data-stu-id="ddc55-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="ddc55-104">В этом учебнике вы узнаете, как toointegrate помочь агент с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddc55-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddc55-105">Вы получаете следующие преимущества от интеграции с Azure AD помогают Scout hello:</span><span class="sxs-lookup"><span data-stu-id="ddc55-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="ddc55-106">В Azure AD можно контролировать, кто имеет доступ tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="ddc55-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="ddc55-107">Можно автоматически войти вашей пользователей tooHelp Scout с помощью единого входа и учетная запись пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddc55-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="ddc55-108">Вы можете управлять учетными записями в один, централизованно, hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc55-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="ddc55-109">toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddc55-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddc55-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ddc55-110">Prerequisites</span></span>

<span data-ttu-id="ddc55-111">tooset интеграции с Azure AD с Scout справки требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ddc55-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="ddc55-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ddc55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddc55-113">подписка Help Scout с включенным единым входом.</span><span class="sxs-lookup"><span data-stu-id="ddc55-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="ddc55-114">Если вы тестируете hello шаги в этом учебнике, мы рекомендуем не проверяют их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ddc55-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="ddc55-115">Рекомендации для тестирования hello шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ddc55-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="ddc55-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ddc55-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="ddc55-117">Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddc55-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddc55-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ddc55-118">Scenario description</span></span>
<span data-ttu-id="ddc55-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ddc55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ddc55-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ddc55-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddc55-121">Добавление справки Scout из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="ddc55-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="ddc55-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddc55-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="ddc55-123">Добавление справки Scout из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="ddc55-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="ddc55-124">tooset копирование hello интеграция справки Scout с Azure AD в галерее hello, добавление справки Scout tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddc55-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ddc55-125">tooadd Scout справки из галереи hello:</span><span class="sxs-lookup"><span data-stu-id="ddc55-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="ddc55-126">В hello [портал Azure](https://portal.azure.com)в левом меню hello, выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="ddc55-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![страница приложений корпоративного Hello][2]
    
3. <span data-ttu-id="ddc55-130">Выберите новое приложение tooadd **новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-130">tooadd a new application, select **New application**.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="ddc55-132">Введите в поле поиска hello, **Scout справки**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="ddc55-133">В результатах поиска hello, выберите **справки Scout**, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Справка Scout в списке результатов hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ddc55-135">Настройка и проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc55-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="ddc55-136">В этом разделе описана настройка и проверка единого входа Azure AD в Help Scout с использованием тестового имени пользователя *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="ddc55-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="ddc55-137">Для единого входа toowork Azure AD необходима пользователя Azure AD аналог tooknow hello в Scout справки.</span><span class="sxs-lookup"><span data-stu-id="ddc55-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="ddc55-138">Связи между пользователя Azure AD и связанных пользователей hello в справке Scout должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="ddc55-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="ddc55-139">tooestablish hello ссылка связи в Scout справки, **Username**, присвойте значение hello hello **имя пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddc55-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="ddc55-140">tooconfigure и теста Azure AD единого входа с Scout справки, полный hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ddc55-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="ddc55-141">[Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="ddc55-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="ddc55-142">Настраивает эту функцию toouse пользователя.</span><span class="sxs-lookup"><span data-stu-id="ddc55-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="ddc55-143">[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="ddc55-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="ddc55-144">Тесты Azure AD единого входа с пользователем hello Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ddc55-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="ddc55-145">[Создание тестового пользователя Help Scout](#create-a-help-scout-test-user)</span><span class="sxs-lookup"><span data-stu-id="ddc55-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="ddc55-146">Создает аналог Саймон Britta Scout справки, связанный toohello представление hello пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddc55-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="ddc55-147">[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="ddc55-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="ddc55-148">Устанавливает toouse Britta Simon Azure AD единого входа.</span><span class="sxs-lookup"><span data-stu-id="ddc55-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddc55-149">[Проверка единого входа](#test-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="ddc55-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="ddc55-150">Подтверждает, что эта конфигурация hello работает.</span><span class="sxs-lookup"><span data-stu-id="ddc55-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="ddc55-151">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc55-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="ddc55-152">В этом разделе можно настроить Azure AD единым входом в портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ddc55-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="ddc55-153">а затем настроите его в приложении Help Scout.</span><span class="sxs-lookup"><span data-stu-id="ddc55-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="ddc55-154">tooset копирование Azure AD единого входа с Scout справки:</span><span class="sxs-lookup"><span data-stu-id="ddc55-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="ddc55-155">В hello в hello портала Azure **справки Scout** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="ddc55-157">На hello **единого входа** страницы, для **режим**выберите **входа на базе SAML**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="ddc55-159">В разделе **URL-адреса и помочь домена Scout**, если требуется tooset приложения hello в режиме инициированный IDP, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ddc55-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="ddc55-160">В hello **идентификатор** введите URL-адрес, имеющий hello следующий шаблон:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ddc55-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="ddc55-161">В hello **URL-адрес ответа** введите URL-адрес, имеющий hello следующий шаблон:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ddc55-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="ddc55-163">Tooset приложения hello в режиме, инициированные SP, установите hello **Показывать дополнительные параметры URL-адреса** флажок, а затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="ddc55-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="ddc55-164">В hello **URL-адрес входа** введите URL-адрес, имеющий следующий формат hello:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="ddc55-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="ddc55-166">значения Hello в эти URL-адреса являются исключительно для демонстрационных целей.</span><span class="sxs-lookup"><span data-stu-id="ddc55-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="ddc55-167">Обновление значений hello hello фактический идентификатор URL-адреса и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="ddc55-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="ddc55-168">обратитесь в службу tooget эти значения [Scout помочь группе поддержки](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="ddc55-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="ddc55-169">В разделе **сертификат подписи SAML**выберите **метаданные в формате XML**и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ddc55-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="ddc55-171">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-171">Select **Save**.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ddc55-173">tooset копирование одного входа на стороне справки Scout hello, отправлять hello загружены метаданные XML файл toohello [Scout помочь группе поддержки](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="ddc55-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="ddc55-174">Группа поддержки справки Scout Hello применяется этот параметр, чтобы правильно настроенной hello SAML единого входа для соединения с обеих сторон.</span><span class="sxs-lookup"><span data-stu-id="ddc55-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ddc55-175">Можно прочитать краткое версии этих инструкций в hello [портал Azure](https://portal.azure.com), тогда как при настройке приложения!</span><span class="sxs-lookup"><span data-stu-id="ddc55-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="ddc55-176">После добавления приложения hello, выбрав **Active Directory** > **корпоративных приложений**выберите hello **Single Sign-On** вкладки. Можно получить доступ к документации hello внедрены в hello **конфигурации** раздел hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="ddc55-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="ddc55-177">Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ddc55-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ddc55-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc55-178">Create an Azure AD test user</span></span>

<span data-ttu-id="ddc55-179">В этом разделе в hello портал Azure Создание тестового пользователя с именем Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ddc55-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="ddc55-181">toocreate тестового пользователя в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ddc55-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="ddc55-182">В hello в левом меню hello, портале Azure выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ddc55-184">toodisplay hello список пользователей, выберите **пользователей и групп**, а затем выберите **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Выбор элементов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ddc55-186">tooopen hello **пользователя** диалоговом вверху hello hello **всех пользователей** выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ddc55-188">В hello **пользователя** диалоговое окно, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ddc55-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="ddc55-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="ddc55-190">В hello **имя пользователя** введите электронный адрес пользователя Саймон Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ddc55-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="ddc55-191">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="ddc55-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="ddc55-192">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-192">Select **Create**.</span></span>

        ![диалоговое окно приветствия пользователя](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="ddc55-194">Создание тестового пользователя Help Scout</span><span class="sxs-lookup"><span data-stu-id="ddc55-194">Create a Help Scout test user</span></span>

<span data-ttu-id="ddc55-195">Hello объекта этого раздела — toocreate пользователя с именем Саймон Britta в Scout справки.</span><span class="sxs-lookup"><span data-stu-id="ddc55-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="ddc55-196">Help Scout поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ddc55-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="ddc55-197">В этом разделе нет не toocomplete действие или задача.</span><span class="sxs-lookup"><span data-stu-id="ddc55-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="ddc55-198">Если пользователь еще не существует в Scout справки, новый создается при попытке tooaccess Scout справки.</span><span class="sxs-lookup"><span data-stu-id="ddc55-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ddc55-199">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ddc55-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ddc55-200">В этом разделе позволяют hello пользователя Britta Simon toouse Azure AD единого входа путем предоставления hello пользователя учетной записи доступа к tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="ddc55-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="ddc55-202">tooassign tooHelp Britta Simon Scout:</span><span class="sxs-lookup"><span data-stu-id="ddc55-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="ddc55-203">В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога.</span><span class="sxs-lookup"><span data-stu-id="ddc55-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="ddc55-204">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ddc55-206">В списке приложений hello выберите **Scout справки**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-206">In hello applications list, select **Help Scout**.</span></span>

    ![ссылку справки Scout Hello в списке приложений hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="ddc55-208">Выберите в меню слева hello, **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hello пользователей и групп каналу][202]

4. <span data-ttu-id="ddc55-210">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-210">Select **Add**.</span></span> <span data-ttu-id="ddc55-211">Затем на hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="ddc55-213">На hello **пользователей и групп** страницы в список пользователей, выберите hello **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ddc55-214">На hello **пользователей и групп** выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="ddc55-215">На hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="ddc55-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ddc55-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ddc55-216">Test single sign-on</span></span>

<span data-ttu-id="ddc55-217">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ddc55-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="ddc55-218">При выборе плитки помогают Scout hello в панель доступа hello вы должны автоматически входить в tooyour Scout справки приложения.</span><span class="sxs-lookup"><span data-stu-id="ddc55-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="ddc55-219">Дополнительные сведения о панели доступа см. в разделе [панели доступа введение toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ddc55-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ddc55-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ddc55-220">Additional resources</span></span>

* [<span data-ttu-id="ddc55-221">Список учебников по toointegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddc55-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddc55-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddc55-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

