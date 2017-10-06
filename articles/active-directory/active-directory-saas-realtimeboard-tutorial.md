---
title: "Руководство по интеграции Azure Active Directory с RealtimeBoard | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: 76644c9ba643d61a903295dea4d417716a47774a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="a7804-103">Руководство по интеграции Azure Active Directory с RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="a7804-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="a7804-104">В этом учебнике вы узнаете, как toointegrate RealtimeBoard с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7804-104">In this tutorial, you learn how toointegrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7804-105">Интеграция с Azure AD RealtimeBoard предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a7804-105">Integrating RealtimeBoard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7804-106">Можно управлять в Azure AD, имеющего доступ tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="a7804-106">You can control in Azure AD who has access tooRealtimeBoard.</span></span>
- <span data-ttu-id="a7804-107">Можно включить на пользователей tooautomatically get вошедшего tooRealtimeBoard (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7804-107">You can enable your users tooautomatically get signed-on tooRealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a7804-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7804-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a7804-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7804-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7804-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7804-110">Prerequisites</span></span>

<span data-ttu-id="a7804-111">tooconfigure интеграция Azure AD с RealtimeBoard требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a7804-111">tooconfigure Azure AD integration with RealtimeBoard, you need hello following items:</span></span>

- <span data-ttu-id="a7804-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a7804-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7804-113">подписка RealtimeBoard с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7804-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7804-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a7804-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7804-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a7804-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7804-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7804-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7804-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7804-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7804-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a7804-118">Scenario description</span></span>
<span data-ttu-id="a7804-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a7804-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7804-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a7804-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7804-121">Добавление RealtimeBoard из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a7804-121">Adding RealtimeBoard from hello gallery</span></span>
2. <span data-ttu-id="a7804-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7804-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-hello-gallery"></a><span data-ttu-id="a7804-123">Добавление RealtimeBoard из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a7804-123">Adding RealtimeBoard from hello gallery</span></span>
<span data-ttu-id="a7804-124">tooconfigure hello интеграции RealtimeBoard в Azure AD, вы должны tooadd RealtimeBoard из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7804-124">tooconfigure hello integration of RealtimeBoard into Azure AD, you need tooadd RealtimeBoard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7804-125">**tooadd RealtimeBoard из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7804-125">**tooadd RealtimeBoard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7804-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a7804-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="a7804-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a7804-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7804-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7804-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="a7804-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a7804-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="a7804-133">Введите в поле поиска hello **RealtimeBoard**выберите **RealtimeBoard** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a7804-133">In hello search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button tooadd hello application.</span></span>

    ![RealtimeBoard в списке результатов hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a7804-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7804-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a7804-136">В этом разделе описана настройка и проверка единого входа Azure AD в RealtimeBoard с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7804-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7804-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в RealtimeBoard является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7804-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RealtimeBoard is tooa user in Azure AD.</span></span> <span data-ttu-id="a7804-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в RealtimeBoard должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a7804-138">In other words, a link relationship between an Azure AD user and hello related user in RealtimeBoard needs toobe established.</span></span>

<span data-ttu-id="a7804-139">В RealtimeBoard, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a7804-139">In RealtimeBoard, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a7804-140">tooconfigure и теста Azure AD единого входа с RealtimeBoard, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a7804-140">tooconfigure and test Azure AD single sign-on with RealtimeBoard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7804-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a7804-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7804-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a7804-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7804-143">**[Создание тестового пользователя RealtimeBoard](#create-a-realtimeboard-test-user)**  -toohave аналог Саймон Britta в RealtimeBoard, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7804-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - toohave a counterpart of Britta Simon in RealtimeBoard that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7804-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a7804-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7804-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7804-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a7804-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7804-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a7804-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="a7804-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="a7804-148">**tooconfigure Azure AD единого входа с RealtimeBoard, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7804-148">**tooconfigure Azure AD single sign-on with RealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7804-149">В hello в hello портала Azure **RealtimeBoard** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a7804-149">In hello Azure portal, on hello **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="a7804-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7804-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="a7804-153">На hello **RealtimeBoard доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="a7804-153">On hello **RealtimeBoard Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="a7804-155">В hello **идентификатор** текстовом поле введите URL-адрес как:`https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="a7804-155">In hello **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="a7804-156">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="a7804-156">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="a7804-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="a7804-158">In hello **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="a7804-159">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7804-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="a7804-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a7804-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a7804-163">tooconfigure единого входа на **RealtimeBoard** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[RealtimeBoard поддержки](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="a7804-163">tooconfigure single sign-on on **RealtimeBoard** side, you need toosend hello downloaded **Metadata XML** too[RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="a7804-164">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="a7804-164">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a7804-165">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a7804-165">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7804-166">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a7804-166">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7804-167">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7804-167">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a7804-168">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7804-168">Create an Azure AD test user</span></span>

<span data-ttu-id="a7804-169">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7804-169">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="a7804-171">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7804-171">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7804-172">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a7804-172">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a7804-174">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a7804-174">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a7804-176">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a7804-176">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a7804-178">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a7804-178">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a7804-180">а.</span><span class="sxs-lookup"><span data-stu-id="a7804-180">a.</span></span> <span data-ttu-id="a7804-181">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7804-181">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7804-182">b.</span><span class="sxs-lookup"><span data-stu-id="a7804-182">b.</span></span> <span data-ttu-id="a7804-183">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a7804-183">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a7804-184">c.</span><span class="sxs-lookup"><span data-stu-id="a7804-184">c.</span></span> <span data-ttu-id="a7804-185">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="a7804-185">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a7804-186">d.</span><span class="sxs-lookup"><span data-stu-id="a7804-186">d.</span></span> <span data-ttu-id="a7804-187">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7804-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="a7804-188">Создание тестового пользователя RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="a7804-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="a7804-189">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="a7804-189">hello objective of this section is toocreate a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="a7804-190">Приложение RealtimeBoard поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a7804-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a7804-191">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a7804-191">There is no action item for you in this section.</span></span> <span data-ttu-id="a7804-192">Если пользователь еще не существует в RealtimeBoard, создается новый, при попытке tooaccess RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="a7804-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt tooaccess RealtimeBoard.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a7804-193">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a7804-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a7804-194">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRealtimeBoard доступа.</span><span class="sxs-lookup"><span data-stu-id="a7804-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRealtimeBoard.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="a7804-196">**tooassign tooRealtimeBoard Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a7804-196">**tooassign Britta Simon tooRealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7804-197">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7804-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a7804-199">В списке приложений hello выберите **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="a7804-199">In hello applications list, select **RealtimeBoard**.</span></span>

    ![ссылка RealtimeBoard Hello в списке приложений hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="a7804-201">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a7804-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="a7804-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7804-203">Click **Add** button.</span></span> <span data-ttu-id="a7804-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7804-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="a7804-206">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a7804-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7804-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a7804-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7804-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a7804-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a7804-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a7804-209">Test single sign-on</span></span>

<span data-ttu-id="a7804-210">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a7804-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7804-211">При нажатии кнопки hello RealtimeBoard плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour RealtimeBoard приложения.</span><span class="sxs-lookup"><span data-stu-id="a7804-211">When you click hello RealtimeBoard tile in hello Access Panel, you should get automatically signed-on tooyour RealtimeBoard application.</span></span>
<span data-ttu-id="a7804-212">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7804-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7804-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7804-213">Additional resources</span></span>

* [<span data-ttu-id="a7804-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7804-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7804-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7804-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

