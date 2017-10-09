---
title: "Руководство. Интеграция Azure Active Directory с Nomadic | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 8c1d3e350ce03c373cf475b2786ec299a7ce5f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="944f9-103">Руководство. Интеграция Azure Active Directory с Nomadic</span><span class="sxs-lookup"><span data-stu-id="944f9-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="944f9-104">В этом учебнике вы узнаете, как toointegrate Nomadic с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="944f9-104">In this tutorial, you learn how toointegrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="944f9-105">Интеграция с Azure AD Nomadic предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="944f9-105">Integrating Nomadic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="944f9-106">Можно управлять в Azure AD, имеющего доступ tooNomadic.</span><span class="sxs-lookup"><span data-stu-id="944f9-106">You can control in Azure AD who has access tooNomadic.</span></span>
- <span data-ttu-id="944f9-107">Можно включить на пользователей tooautomatically get вошедшего tooNomadic (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="944f9-107">You can enable your users tooautomatically get signed-on tooNomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="944f9-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="944f9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="944f9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="944f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="944f9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="944f9-110">Prerequisites</span></span>

<span data-ttu-id="944f9-111">tooconfigure интеграция Azure AD с Nomadic требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="944f9-111">tooconfigure Azure AD integration with Nomadic, you need hello following items:</span></span>

- <span data-ttu-id="944f9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="944f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="944f9-113">подписка Nomadic с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="944f9-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="944f9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="944f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="944f9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="944f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="944f9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="944f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="944f9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="944f9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="944f9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="944f9-118">Scenario description</span></span>
<span data-ttu-id="944f9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="944f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="944f9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="944f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="944f9-121">Добавление Nomadic из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="944f9-121">Add Nomadic from hello gallery</span></span>
2. <span data-ttu-id="944f9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="944f9-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-hello-gallery"></a><span data-ttu-id="944f9-123">Добавление Nomadic из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="944f9-123">Add Nomadic from hello gallery</span></span>
<span data-ttu-id="944f9-124">tooconfigure hello интеграции Nomadic в Azure AD, вы должны tooadd Nomadic из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="944f9-124">tooconfigure hello integration of Nomadic into Azure AD, you need tooadd Nomadic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="944f9-125">**tooadd Nomadic из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="944f9-125">**tooadd Nomadic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="944f9-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="944f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="944f9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="944f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="944f9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="944f9-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="944f9-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="944f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="944f9-133">Введите в поле поиска hello **Nomadic**выберите **Nomadic** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="944f9-133">In hello search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button tooadd hello application.</span></span>

    ![В списке результатов hello nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="944f9-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="944f9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="944f9-136">В этом разделе описана настройка и проверка единого входа Azure AD в Nomadic с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="944f9-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="944f9-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Nomadic является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="944f9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadic is tooa user in Azure AD.</span></span> <span data-ttu-id="944f9-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Nomadic должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="944f9-138">In other words, a link relationship between an Azure AD user and hello related user in Nomadic needs toobe established.</span></span>

<span data-ttu-id="944f9-139">В Nomadic, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="944f9-139">In Nomadic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="944f9-140">tooconfigure и теста Azure AD единого входа с Nomadic, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="944f9-140">tooconfigure and test Azure AD single sign-on with Nomadic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="944f9-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="944f9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="944f9-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="944f9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="944f9-143">**[Создание Nomadic тестового пользователя](#create-a-nomadic-test-user)**  -toohave аналог Саймон Britta в Nomadic, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="944f9-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - toohave a counterpart of Britta Simon in Nomadic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="944f9-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="944f9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="944f9-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="944f9-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="944f9-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="944f9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="944f9-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Nomadic.</span><span class="sxs-lookup"><span data-stu-id="944f9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="944f9-148">**tooconfigure Azure AD единого входа с Nomadic, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="944f9-148">**tooconfigure Azure AD single sign-on with Nomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="944f9-149">В hello в hello портала Azure **Nomadic** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="944f9-149">In hello Azure portal, on hello **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="944f9-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="944f9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="944f9-153">На hello **Nomadic доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="944f9-153">On hello **Nomadic Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="944f9-155">а.</span><span class="sxs-lookup"><span data-stu-id="944f9-155">a.</span></span> <span data-ttu-id="944f9-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="944f9-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="944f9-157">b.</span><span class="sxs-lookup"><span data-stu-id="944f9-157">b.</span></span> <span data-ttu-id="944f9-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="944f9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="944f9-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="944f9-159">These values are not real.</span></span> <span data-ttu-id="944f9-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="944f9-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="944f9-161">Обратитесь к [Nomadic клиента поддержки](mailto:help@nomadic.fm) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="944f9-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) tooget these values.</span></span> 
 


4. <span data-ttu-id="944f9-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="944f9-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="944f9-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="944f9-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="944f9-166">tooget SSO настроен для вашего приложения, обратитесь в службу [Nomadic поддержки](mailto:help@nomadic.fm) и предоставить им загружаются hello **метаданные**.</span><span class="sxs-lookup"><span data-stu-id="944f9-166">tooget SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with hello downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="944f9-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="944f9-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="944f9-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="944f9-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="944f9-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="944f9-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="944f9-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="944f9-170">Create an Azure AD test user</span></span>

<span data-ttu-id="944f9-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="944f9-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="944f9-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="944f9-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="944f9-174">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="944f9-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="944f9-176">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="944f9-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="944f9-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="944f9-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="944f9-180">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="944f9-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="944f9-182">а.</span><span class="sxs-lookup"><span data-stu-id="944f9-182">a.</span></span> <span data-ttu-id="944f9-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="944f9-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="944f9-184">b.</span><span class="sxs-lookup"><span data-stu-id="944f9-184">b.</span></span> <span data-ttu-id="944f9-185">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="944f9-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="944f9-186">c.</span><span class="sxs-lookup"><span data-stu-id="944f9-186">c.</span></span> <span data-ttu-id="944f9-187">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="944f9-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="944f9-188">d.</span><span class="sxs-lookup"><span data-stu-id="944f9-188">d.</span></span> <span data-ttu-id="944f9-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="944f9-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="944f9-190">Создание тестового пользователя в Nomadic</span><span class="sxs-lookup"><span data-stu-id="944f9-190">Create a Nomadic test user</span></span>

<span data-ttu-id="944f9-191">В этом разделе описано, как создать пользователя Britta Simon в приложении Nomadic.</span><span class="sxs-lookup"><span data-stu-id="944f9-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="944f9-192">Можно работать с [Nomadic поддержки](mailto:help@nomadic.fm) tooadd hello пользователей на платформе Nomadic hello.</span><span class="sxs-lookup"><span data-stu-id="944f9-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) tooadd hello users in hello Nomadic platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="944f9-193">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="944f9-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="944f9-194">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNomadic доступа.</span><span class="sxs-lookup"><span data-stu-id="944f9-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadic.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="944f9-196">**tooassign tooNomadic Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="944f9-196">**tooassign Britta Simon tooNomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="944f9-197">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="944f9-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="944f9-199">В списке приложений hello выберите **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="944f9-199">In hello applications list, select **Nomadic**.</span></span>

    ![Hello Nomadic ссылку в списке приложений hello](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="944f9-201">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="944f9-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="944f9-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="944f9-203">Click **Add** button.</span></span> <span data-ttu-id="944f9-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="944f9-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="944f9-206">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="944f9-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="944f9-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="944f9-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="944f9-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="944f9-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="944f9-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="944f9-209">Test single sign-on</span></span>

<span data-ttu-id="944f9-210">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="944f9-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="944f9-211">При нажатии кнопки Nomadic плитки hello в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour Nomadic приложения.</span><span class="sxs-lookup"><span data-stu-id="944f9-211">When you click hello Nomadic tile in hello Access Panel, you should get automatically signed-on tooyour Nomadic application.</span></span>
<span data-ttu-id="944f9-212">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="944f9-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="944f9-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="944f9-213">Additional resources</span></span>

* [<span data-ttu-id="944f9-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="944f9-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="944f9-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="944f9-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

