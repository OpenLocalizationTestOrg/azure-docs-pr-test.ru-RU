---
title: "Руководство. Интеграция Azure Active Directory с Brightspace (разработка Desire2Learn) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Brightspace by Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 99d03dc50defcb291a651a5415e30baab39e1e77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="3b9b4-103">Руководство. Интеграция Azure Active Directory с Brightspace (разработка Desire2Learn)</span><span class="sxs-lookup"><span data-stu-id="3b9b4-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="3b9b4-104">В этом учебнике вы узнаете, как toointegrate Brightspace by Desire2Learn с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-104">In this tutorial, you learn how toointegrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b9b4-105">Интеграция Brightspace by Desire2Learn с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3b9b4-106">Можно управлять в Azure AD, имеющего доступ tooBrightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="3b9b4-106">You can control in Azure AD who has access tooBrightspace by Desire2Learn</span></span>
- <span data-ttu-id="3b9b4-107">Можно включить на пользователей tooautomatically get вошедшего tooBrightspace by Desire2Learn (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b9b4-107">You can enable your users tooautomatically get signed-on tooBrightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b9b4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3b9b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3b9b4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b9b4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b9b4-110">Prerequisites</span></span>

<span data-ttu-id="3b9b4-111">tooconfigure интеграция Azure AD с Brightspace by Desire2Learn требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-111">tooconfigure Azure AD integration with Brightspace by Desire2Learn, you need hello following items:</span></span>

- <span data-ttu-id="3b9b4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3b9b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b9b4-113">Подписка с поддержкой единого входа Brightspace (разработка Desire2Learn)</span><span class="sxs-lookup"><span data-stu-id="3b9b4-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b9b4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b9b4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b9b4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b9b4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b9b4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3b9b4-118">Scenario description</span></span>
<span data-ttu-id="3b9b4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b9b4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b9b4-121">Добавление Brightspace by Desire2Learn из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3b9b4-121">Adding Brightspace by Desire2Learn from hello gallery</span></span>
2. <span data-ttu-id="3b9b4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b9b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-hello-gallery"></a><span data-ttu-id="3b9b4-123">Добавление Brightspace by Desire2Learn из галереи hello</span><span class="sxs-lookup"><span data-stu-id="3b9b4-123">Adding Brightspace by Desire2Learn from hello gallery</span></span>
<span data-ttu-id="3b9b4-124">tooconfigure hello интеграцией Brightspace by Desire2Learn с Azure AD, вы должны tooadd Brightspace by Desire2Learn из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-124">tooconfigure hello integration of Brightspace by Desire2Learn into Azure AD, you need tooadd Brightspace by Desire2Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3b9b4-125">**tooadd Brightspace by Desire2Learn из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b9b4-125">**tooadd Brightspace by Desire2Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b9b4-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b9b4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3b9b4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3b9b4-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3b9b4-133">Введите в поле поиска hello **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-133">In hello search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="3b9b4-135">В панели результатов hello выберите **Brightspace by Desire2Learn**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-135">In hello results panel, select **Brightspace by Desire2Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b9b4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b9b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b9b4-138">В этом разделе описана настройка и проверка единого входа Azure AD в Brightspace by Desire2Learn с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b9b4-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Brightspace by Desire2Learn является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Brightspace by Desire2Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="3b9b4-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Brightspace by Desire2Learn должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-140">In other words, a link relationship between an Azure AD user and hello related user in Brightspace by Desire2Learn needs toobe established.</span></span>

<span data-ttu-id="3b9b4-141">В Brightspace by Desire2Learn присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-141">In Brightspace by Desire2Learn, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3b9b4-142">tooconfigure и теста Azure AD единого входа с Brightspace by Desire2Learn, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-142">tooconfigure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3b9b4-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3b9b4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b9b4-145">**[Создание Brightspace by Desire2Learn тестового пользователя](#creating-a-brightspace-by-desire2learn-test-user)**  -toohave аналог Саймон Britta в Brightspace by Desire2Learn, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - toohave a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b9b4-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b9b4-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b9b4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b9b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b9b4-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Brightspace Desire2Learn приложением.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="3b9b4-150">**Azure AD tooconfigure единого входа с Brightspace by Desire2Learn, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b9b4-150">**tooconfigure Azure AD single sign-on with Brightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b9b4-151">В hello в hello портала Azure **Brightspace by Desire2Learn** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-151">In hello Azure portal, on hello **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3b9b4-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="3b9b4-155">На hello **Brightspace by Desire2Learn доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-155">On hello **Brightspace by Desire2Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="3b9b4-157">а.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-157">a.</span></span> <span data-ttu-id="3b9b4-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="3b9b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-159">b.</span></span> <span data-ttu-id="3b9b4-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="3b9b4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3b9b4-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-161">These values are not real.</span></span> <span data-ttu-id="3b9b4-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="3b9b4-163">Обратитесь к [Brightspace by Desire2Learn поддержки](https://www.d2l.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) tooget these values.</span></span>
 


4. <span data-ttu-id="3b9b4-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="3b9b4-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3b9b4-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b9b4-168">tooconfigure единого входа на **Brightspace by Desire2Learn** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Brightspace by Desire2Learn поддержки](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-168">tooconfigure single sign-on on **Brightspace by Desire2Learn** side, you need toosend hello downloaded **Metadata XML** too[Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="3b9b4-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="3b9b4-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3b9b4-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3b9b4-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b9b4-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b9b4-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b9b4-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b9b4-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3b9b4-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b9b4-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b9b4-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b9b4-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b9b4-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="3b9b4-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b9b4-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3b9b4-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b9b4-184">а.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-184">a.</span></span> <span data-ttu-id="3b9b4-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b9b4-186">b.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-186">b.</span></span> <span data-ttu-id="3b9b4-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b9b4-188">c.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-188">c.</span></span> <span data-ttu-id="3b9b4-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3b9b4-190">d.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-190">d.</span></span> <span data-ttu-id="3b9b4-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="3b9b4-192">Создание тестового пользователя Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="3b9b4-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="3b9b4-193">В порядке toolog tooenable Azure AD пользователи в Brightspace by Desire2Learn их необходимо подготовить в Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-193">In order tooenable Azure AD users toolog into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="3b9b4-194">В случае Brightspace by Desire2Learn с hello, учетные записи пользователей hello должны toobe, созданные вашей [Brightspace by Desire2Learn поддержки](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-194">In hello case of Brightspace by Desire2Learn, hello user accounts need toobe created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="3b9b4-195">Можно использовать любые другие Brightspace, средства создания учетных записей пользователя Desire2Learn или API, предоставленные Brightspace по Desire2Learn tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3b9b4-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="3b9b4-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3b9b4-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooBrightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBrightspace by Desire2Learn.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3b9b4-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="3b9b4-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="3b9b4-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3b9b4-202">В списке приложений hello выберите **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-202">In hello applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="3b9b4-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3b9b4-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-206">Click **Add** button.</span></span> <span data-ttu-id="3b9b4-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3b9b4-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3b9b4-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b9b4-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b9b4-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3b9b4-212">Testing single sign-on</span></span>

<span data-ttu-id="3b9b4-213">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3b9b4-214">При нажатии кнопки hello Brightspace по Desire2Learn плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Brightspace Desire2Learn приложением.</span><span class="sxs-lookup"><span data-stu-id="3b9b4-214">When you click hello Brightspace by Desire2Learn tile in hello Access Panel, you should get automatically signed-on tooyour Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="3b9b4-215">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3b9b4-215">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b9b4-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3b9b4-216">Additional resources</span></span>

* [<span data-ttu-id="3b9b4-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b9b4-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b9b4-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b9b4-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

