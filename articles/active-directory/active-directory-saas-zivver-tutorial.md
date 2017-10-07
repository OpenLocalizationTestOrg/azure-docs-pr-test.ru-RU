---
title: "Руководство. Интеграция Azure Active Directory с ZIVVER | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ZIVVER."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 0928abcc4dcbd97b892298f4919c8d44e1a058a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="716af-103">Руководство. Интеграция Azure Active Directory с ZIVVER</span><span class="sxs-lookup"><span data-stu-id="716af-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="716af-104">В этом учебнике вы узнаете, как toointegrate ZIVVER с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="716af-104">In this tutorial, you learn how toointegrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="716af-105">Интеграция с Azure AD ZIVVER предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="716af-105">Integrating ZIVVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="716af-106">Можно управлять в Azure AD, имеющего доступ tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="716af-106">You can control in Azure AD who has access tooZIVVER.</span></span>
- <span data-ttu-id="716af-107">Можно включить на пользователей tooautomatically get вошедшего tooZIVVER (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="716af-107">You can enable your users tooautomatically get signed-on tooZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="716af-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="716af-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="716af-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="716af-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="716af-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="716af-110">Prerequisites</span></span>

<span data-ttu-id="716af-111">tooconfigure интеграция Azure AD с ZIVVER требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="716af-111">tooconfigure Azure AD integration with ZIVVER, you need hello following items:</span></span>

- <span data-ttu-id="716af-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="716af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="716af-113">подписка с поддержкой единого входа ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="716af-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="716af-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="716af-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="716af-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="716af-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="716af-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="716af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="716af-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="716af-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="716af-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="716af-118">Scenario description</span></span>
<span data-ttu-id="716af-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="716af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="716af-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="716af-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="716af-121">Добавление ZIVVER из галереи hello</span><span class="sxs-lookup"><span data-stu-id="716af-121">Adding ZIVVER from hello gallery</span></span>
2. <span data-ttu-id="716af-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="716af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-hello-gallery"></a><span data-ttu-id="716af-123">Добавление ZIVVER из галереи hello</span><span class="sxs-lookup"><span data-stu-id="716af-123">Adding ZIVVER from hello gallery</span></span>
<span data-ttu-id="716af-124">tooconfigure hello интеграции ZIVVER в Azure AD, вы должны tooadd ZIVVER из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="716af-124">tooconfigure hello integration of ZIVVER into Azure AD, you need tooadd ZIVVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="716af-125">**tooadd ZIVVER из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="716af-125">**tooadd ZIVVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="716af-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="716af-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="716af-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="716af-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="716af-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="716af-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="716af-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="716af-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="716af-133">Введите в поле поиска hello **ZIVVER**выберите **ZIVVER** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="716af-133">In hello search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ZIVVER в списке результатов hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="716af-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="716af-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="716af-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ZIVVER с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="716af-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="716af-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ZIVVER является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="716af-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ZIVVER is tooa user in Azure AD.</span></span> <span data-ttu-id="716af-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ZIVVER должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="716af-138">In other words, a link relationship between an Azure AD user and hello related user in ZIVVER needs toobe established.</span></span>

<span data-ttu-id="716af-139">В ZIVVER, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="716af-139">In ZIVVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="716af-140">tooconfigure и теста Azure AD единого входа с ZIVVER, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="716af-140">tooconfigure and test Azure AD single sign-on with ZIVVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="716af-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="716af-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="716af-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="716af-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="716af-143">**[Создание тестового пользователя ZIVVER](#create-a-zivver-test-user)**  -toohave аналог Саймон Britta в ZIVVER, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="716af-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - toohave a counterpart of Britta Simon in ZIVVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="716af-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="716af-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="716af-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="716af-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="716af-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="716af-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="716af-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="716af-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="716af-148">**tooconfigure Azure AD единого входа с ZIVVER, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="716af-148">**tooconfigure Azure AD single sign-on with ZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="716af-149">В hello в hello портала Azure **ZIVVER** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="716af-149">In hello Azure portal, on hello **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="716af-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="716af-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="716af-153">На hello **URL-адреса и домена ZIVVER** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="716af-153">On hello **ZIVVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="716af-155">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="716af-155">In hello **Identifier** textbox, type hello URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="716af-156">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="716af-156">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="716af-158">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="716af-158">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="716af-160">tooconfigure единого входа на **ZIVVER** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[ZIVVER поддержки](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="716af-160">tooconfigure single sign-on on **ZIVVER** side, you need toosend hello downloaded **Metadata XML** too[ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="716af-161">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="716af-161">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="716af-162">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="716af-162">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="716af-163">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="716af-163">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="716af-164">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="716af-164">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="716af-165">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="716af-165">Create an Azure AD test user</span></span>

<span data-ttu-id="716af-166">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="716af-166">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="716af-168">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="716af-168">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="716af-169">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="716af-169">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="716af-171">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="716af-171">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="716af-173">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="716af-173">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="716af-175">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="716af-175">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="716af-177">а.</span><span class="sxs-lookup"><span data-stu-id="716af-177">a.</span></span> <span data-ttu-id="716af-178">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="716af-178">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="716af-179">b.</span><span class="sxs-lookup"><span data-stu-id="716af-179">b.</span></span> <span data-ttu-id="716af-180">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="716af-180">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="716af-181">c.</span><span class="sxs-lookup"><span data-stu-id="716af-181">c.</span></span> <span data-ttu-id="716af-182">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="716af-182">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="716af-183">d.</span><span class="sxs-lookup"><span data-stu-id="716af-183">d.</span></span> <span data-ttu-id="716af-184">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="716af-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="716af-185">Создание тестового пользователя ZIVVER</span><span class="sxs-lookup"><span data-stu-id="716af-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="716af-186">В этом разделе описано, как создать пользователя Britta Simon в приложении ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="716af-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="716af-187">Работать с [ZIVVER поддержки](https://support.zivver.com) tooadd hello пользователей на платформе ZIVVER hello.</span><span class="sxs-lookup"><span data-stu-id="716af-187">Work with [ZIVVER support team](https://support.zivver.com) tooadd hello users in hello ZIVVER platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="716af-188">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="716af-188">Assign hello Azure AD test user</span></span>

<span data-ttu-id="716af-189">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZIVVER доступа.</span><span class="sxs-lookup"><span data-stu-id="716af-189">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZIVVER.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="716af-191">**tooassign tooZIVVER Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="716af-191">**tooassign Britta Simon tooZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="716af-192">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="716af-192">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="716af-194">В списке приложений hello выберите **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="716af-194">In hello applications list, select **ZIVVER**.</span></span>

    ![ссылка ZIVVER Hello в списке приложений hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="716af-196">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="716af-196">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="716af-198">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="716af-198">Click **Add** button.</span></span> <span data-ttu-id="716af-199">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="716af-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="716af-201">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="716af-201">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="716af-202">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="716af-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="716af-203">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="716af-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="716af-204">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="716af-204">Test single sign-on</span></span>

<span data-ttu-id="716af-205">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="716af-205">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="716af-206">При нажатии кнопки ZIVVER плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour ZIVVER приложения.</span><span class="sxs-lookup"><span data-stu-id="716af-206">When you click hello ZIVVER tile in hello Access Panel, you should get automatically signed-on tooyour ZIVVER application.</span></span>
<span data-ttu-id="716af-207">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="716af-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="716af-208">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="716af-208">Additional resources</span></span>

* [<span data-ttu-id="716af-209">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="716af-209">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="716af-210">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="716af-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

