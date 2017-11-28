---
title: "Руководство. Интеграция Azure Active Directory с WORKS MOBILE | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и MOBILE работает."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="a8fa7-103">Руководство. Интеграция Azure Active Directory с WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="a8fa7-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="a8fa7-104">В этом учебнике вы узнаете, как работает toointegrate МОБИЛЬНЫЕ приложения с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8fa7-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8fa7-105">Интеграция мобильных устройств работает с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a8fa7-106">Можно управлять в Azure AD, имеющего доступ tooWORKS мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="a8fa7-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="a8fa7-107">Можно включить на пользователей tooautomatically get вошедшего tooWORKS MOBILE (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8fa7-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8fa7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a8fa7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a8fa7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8fa7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8fa7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8fa7-110">Prerequisites</span></span>

<span data-ttu-id="a8fa7-111">tooconfigure интеграция Azure AD с мобильных устройств работает, необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="a8fa7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a8fa7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8fa7-113">подписка WORKS MOBILE с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8fa7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8fa7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8fa7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8fa7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8fa7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8fa7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a8fa7-118">Scenario description</span></span>
<span data-ttu-id="a8fa7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8fa7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8fa7-121">Добавление МОБИЛЬНЫХ WORKS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a8fa7-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="a8fa7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8fa7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="a8fa7-123">Добавление МОБИЛЬНЫХ WORKS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a8fa7-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="a8fa7-124">tooconfigure hello интеграции MOBILE работает в Azure AD, вы должны tooadd WORKS MOBILE из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a8fa7-125">**tooadd MOBILE WORKS из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8fa7-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8fa7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a8fa7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a8fa7-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a8fa7-133">Введите в поле поиска hello **MOBILE работает**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="a8fa7-135">В панели результатов hello выберите **MOBILE работает**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8fa7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8fa7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8fa7-138">В этом разделе описывается настройка и проверка единого входа Azure AD в WORKS MOBILE с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8fa7-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в WORKS MOBILE является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="a8fa7-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в WORKS MOBILE должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="a8fa7-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в MOBILE работает.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="a8fa7-142">tooconfigure и теста Azure AD единого входа с мобильных устройств работает, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a8fa7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a8fa7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8fa7-145">**[Создание тестового пользователя MOBILE работает](#creating-a-works-mobile-test-user)**  -toohave аналог Саймон Britta в MOBILE работает, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8fa7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8fa7-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8fa7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8fa7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8fa7-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении работает MOBILE.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="a8fa7-150">**Azure AD tooconfigure единого входа с мобильных устройств работает, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8fa7-151">В hello в hello портала Azure **MOBILE работает** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a8fa7-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="a8fa7-155">На hello **URL-адреса и домена MOBILE работает** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="a8fa7-157">а.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-157">a.</span></span> <span data-ttu-id="a8fa7-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="a8fa7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="a8fa7-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-159">b.</span></span> <span data-ttu-id="a8fa7-160">В hello **идентификатор** текстовое поле, значение типа hello как`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="a8fa7-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8fa7-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-161">This value is not real.</span></span> <span data-ttu-id="a8fa7-162">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a8fa7-163">Обратитесь к [клиент MOBILE работает группа поддержки](mailto:dl_ssoinfo@worksmobile.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="a8fa7-164">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="a8fa7-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a8fa7-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8fa7-168">На hello **конфигурация МОБИЛЬНЫХ WORKS** щелкните **Настройка MOBILE работает** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a8fa7-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="a8fa7-171">tooget SSO настроен для вашего приложения, обратитесь в службу [MOBILE работает группа поддержки](mailto:dl_ssoinfo@worksmobile.com) и предоставить им hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="a8fa7-172">• hello загружены **файл сертификата**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="a8fa7-173">• hello **SAML единого входа URL-адрес службы**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="a8fa7-174">• hello **SAML идентификатор сущности**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="a8fa7-175">• hello **URL-адрес выхода**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="a8fa7-176">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a8fa7-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a8fa7-177">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a8fa7-178">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8fa7-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8fa7-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8fa7-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8fa7-180">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a8fa7-182">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8fa7-183">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8fa7-185">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8fa7-187">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a8fa7-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8fa7-189">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a8fa7-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8fa7-191">а.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-191">a.</span></span> <span data-ttu-id="a8fa7-192">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8fa7-193">b.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-193">b.</span></span> <span data-ttu-id="a8fa7-194">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8fa7-195">c.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-195">c.</span></span> <span data-ttu-id="a8fa7-196">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a8fa7-197">d.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-197">d.</span></span> <span data-ttu-id="a8fa7-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="a8fa7-199">Создание тестового пользователя WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="a8fa7-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="a8fa7-200">В этом разделе описано, как создать пользователя Britta Simon в приложении WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="a8fa7-201">Можно работать с [MOBILE работает группа поддержки](mailto:dl_ssoinfo@worksmobile.com) tooadd hello пользователей в платформу WORKS MOBILE hello.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a8fa7-202">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a8fa7-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a8fa7-203">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a8fa7-205">**tooassign tooWORKS Britta Simon мобильных устройств, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a8fa7-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="a8fa7-206">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a8fa7-208">В списке приложений hello выберите **MOBILE работает**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="a8fa7-210">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a8fa7-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-212">Click **Add** button.</span></span> <span data-ttu-id="a8fa7-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a8fa7-215">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a8fa7-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8fa7-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8fa7-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a8fa7-218">Testing single sign-on</span></span>

<span data-ttu-id="a8fa7-219">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a8fa7-220">Если щелкнуть плитку WORKS MOBILE hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего WORKS МОБИЛЬНОГО приложения.</span><span class="sxs-lookup"><span data-stu-id="a8fa7-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="a8fa7-221">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8fa7-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a8fa7-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8fa7-222">Additional resources</span></span>

* [<span data-ttu-id="a8fa7-223">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8fa7-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8fa7-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8fa7-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

