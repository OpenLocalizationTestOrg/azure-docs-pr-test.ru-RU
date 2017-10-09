---
title: "Руководство. Интеграция Azure Active Directory с Oneteam | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 7964aaaf9b9570d460f28d86de34b5e87693ba93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="da336-103">Руководство. Интеграция Azure Active Directory с Oneteam</span><span class="sxs-lookup"><span data-stu-id="da336-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="da336-104">В этом учебнике вы узнаете, как toointegrate Oneteam с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da336-104">In this tutorial, you learn how toointegrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da336-105">Интеграция с Azure AD Oneteam предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="da336-105">Integrating Oneteam with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da336-106">Можно управлять в Azure AD, имеющего доступ tooOneteam</span><span class="sxs-lookup"><span data-stu-id="da336-106">You can control in Azure AD who has access tooOneteam</span></span>
- <span data-ttu-id="da336-107">Можно включить на пользователей tooautomatically get вошедшего tooOneteam (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="da336-107">You can enable your users tooautomatically get signed-on tooOneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da336-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="da336-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="da336-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da336-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da336-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="da336-110">Prerequisites</span></span>

<span data-ttu-id="da336-111">tooconfigure интеграция Azure AD с Oneteam требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="da336-111">tooconfigure Azure AD integration with Oneteam, you need hello following items:</span></span>

- <span data-ttu-id="da336-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="da336-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da336-113">подписка Oneteam с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="da336-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da336-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="da336-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da336-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="da336-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da336-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="da336-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da336-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da336-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da336-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="da336-118">Scenario description</span></span>
<span data-ttu-id="da336-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="da336-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da336-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="da336-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da336-121">Добавление Oneteam из галереи hello</span><span class="sxs-lookup"><span data-stu-id="da336-121">Adding Oneteam from hello gallery</span></span>
2. <span data-ttu-id="da336-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da336-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-hello-gallery"></a><span data-ttu-id="da336-123">Добавление Oneteam из галереи hello</span><span class="sxs-lookup"><span data-stu-id="da336-123">Adding Oneteam from hello gallery</span></span>
<span data-ttu-id="da336-124">tooconfigure hello интеграции Oneteam в Azure AD, вы должны tooadd Oneteam из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="da336-124">tooconfigure hello integration of Oneteam into Azure AD, you need tooadd Oneteam from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da336-125">**tooadd Oneteam из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da336-125">**tooadd Oneteam from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da336-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="da336-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da336-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="da336-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da336-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="da336-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="da336-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="da336-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="da336-133">Введите в поле поиска hello **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="da336-133">In hello search box, type **Oneteam**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="da336-135">В панели результатов hello выберите **Oneteam**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="da336-135">In hello results panel, select **Oneteam**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da336-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da336-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da336-138">В этом разделе описана настройка и проверка единого входа Azure AD в Oneteam с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da336-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da336-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Oneteam является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da336-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Oneteam is tooa user in Azure AD.</span></span> <span data-ttu-id="da336-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Oneteam должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="da336-140">In other words, a link relationship between an Azure AD user and hello related user in Oneteam needs toobe established.</span></span>

<span data-ttu-id="da336-141">В Oneteam, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="da336-141">In Oneteam, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="da336-142">tooconfigure и теста Azure AD единого входа с Oneteam, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="da336-142">tooconfigure and test Azure AD single sign-on with Oneteam, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da336-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="da336-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da336-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="da336-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da336-145">**[Создание тестового пользователя Oneteam](#creating-a-oneteam-test-user)**  -toohave аналог Саймон Britta в Oneteam, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="da336-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - toohave a counterpart of Britta Simon in Oneteam that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="da336-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="da336-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da336-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="da336-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da336-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="da336-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da336-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Oneteam.</span><span class="sxs-lookup"><span data-stu-id="da336-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="da336-150">**tooconfigure Azure AD единого входа с Oneteam, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da336-150">**tooconfigure Azure AD single sign-on with Oneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="da336-151">В hello в hello портала Azure **Oneteam** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="da336-151">In hello Azure portal, on hello **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="da336-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="da336-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="da336-155">На hello **Oneteam доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="da336-155">On hello **Oneteam Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="da336-157">а.</span><span class="sxs-lookup"><span data-stu-id="da336-157">a.</span></span> <span data-ttu-id="da336-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="da336-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="da336-159">b.</span><span class="sxs-lookup"><span data-stu-id="da336-159">b.</span></span> <span data-ttu-id="da336-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="da336-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="da336-161">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="da336-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="da336-163">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="da336-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="da336-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="da336-164">These values are not real.</span></span> <span data-ttu-id="da336-165">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="da336-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="da336-166">Обратитесь к [группа поддержки клиента Oneteam](https://support.one-team.com/hc/requests/new) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="da336-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) tooget these values.</span></span> 



5. <span data-ttu-id="da336-167">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="da336-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="da336-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="da336-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="da336-171">tooget единого входа, настроенному для вашего приложения могут вызывать hello в службу поддержки с [Oneteam поддержки](https://support.one-team.com/hc/requests/new) и сообщите hello загружены **метаданные**.</span><span class="sxs-lookup"><span data-stu-id="da336-171">tooget SSO configured for your application, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them hello downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="da336-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="da336-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="da336-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="da336-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="da336-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da336-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da336-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="da336-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="da336-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="da336-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="da336-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da336-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da336-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="da336-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da336-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="da336-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da336-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="da336-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da336-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="da336-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da336-187">а.</span><span class="sxs-lookup"><span data-stu-id="da336-187">a.</span></span> <span data-ttu-id="da336-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da336-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da336-189">b.</span><span class="sxs-lookup"><span data-stu-id="da336-189">b.</span></span> <span data-ttu-id="da336-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da336-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da336-191">c.</span><span class="sxs-lookup"><span data-stu-id="da336-191">c.</span></span> <span data-ttu-id="da336-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="da336-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="da336-193">d.</span><span class="sxs-lookup"><span data-stu-id="da336-193">d.</span></span> <span data-ttu-id="da336-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="da336-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="da336-195">Создание тестового пользователя Oneteam</span><span class="sxs-lookup"><span data-stu-id="da336-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="da336-196">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Oneteam.</span><span class="sxs-lookup"><span data-stu-id="da336-196">hello objective of this section is toocreate a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="da336-197">Приложение Oneteam поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="da336-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="da336-198">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="da336-198">There is no action item for you in this section.</span></span> <span data-ttu-id="da336-199">Если он еще не существует во время попытки tooaccess Oneteam, создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="da336-199">A new user will be created during an attempt tooaccess Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="da336-200">Если вам требуется toocreate пользователя вручную, могут вызывать hello в службу поддержки с [Oneteam поддержки](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="da336-200">If you need toocreate an user manually, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="da336-201">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="da336-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="da336-202">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOneteam доступа.</span><span class="sxs-lookup"><span data-stu-id="da336-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOneteam.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="da336-204">**tooassign tooOneteam Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="da336-204">**tooassign Britta Simon tooOneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="da336-205">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="da336-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="da336-207">В списке приложений hello выберите **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="da336-207">In hello applications list, select **Oneteam**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="da336-209">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="da336-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="da336-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="da336-211">Click **Add** button.</span></span> <span data-ttu-id="da336-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="da336-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="da336-214">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="da336-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da336-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="da336-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da336-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="da336-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da336-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="da336-217">Testing single sign-on</span></span>

<span data-ttu-id="da336-218">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="da336-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="da336-219">При нажатии кнопки hello Oneteam плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Oneteam приложения.</span><span class="sxs-lookup"><span data-stu-id="da336-219">When you click hello Oneteam tile in hello Access Panel, you should get automatically signed-on tooyour Oneteam application.</span></span>
<span data-ttu-id="da336-220">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da336-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="da336-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="da336-221">Additional resources</span></span>

* [<span data-ttu-id="da336-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da336-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da336-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da336-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

