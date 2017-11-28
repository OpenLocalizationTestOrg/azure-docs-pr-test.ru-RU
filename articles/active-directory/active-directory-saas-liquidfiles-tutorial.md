---
title: "Руководство по интеграции Azure Active Directory с LiquidFiles | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="1b114-103">Руководство по интеграции Azure Active Directory с LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="1b114-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="1b114-104">В этом учебнике вы узнаете, как toointegrate LiquidFiles с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b114-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b114-105">Интеграция с Azure AD LiquidFiles предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1b114-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b114-106">Можно управлять в Azure AD, имеющего доступ tooLiquidFiles</span><span class="sxs-lookup"><span data-stu-id="1b114-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="1b114-107">Можно включить на пользователей tooautomatically get вошедшего tooLiquidFiles (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b114-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b114-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1b114-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1b114-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b114-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b114-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b114-110">Prerequisites</span></span>

<span data-ttu-id="1b114-111">tooconfigure интеграция Azure AD с LiquidFiles требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1b114-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="1b114-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1b114-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b114-113">подписка LiquidFiles с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1b114-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b114-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1b114-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b114-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1b114-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b114-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1b114-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b114-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b114-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b114-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1b114-118">Scenario description</span></span>
<span data-ttu-id="1b114-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1b114-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b114-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1b114-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b114-121">Добавление LiquidFiles из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1b114-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="1b114-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b114-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="1b114-123">Добавление LiquidFiles из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1b114-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="1b114-124">tooconfigure hello интеграции LiquidFiles в Azure AD, вы должны tooadd LiquidFiles из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1b114-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b114-125">**tooadd LiquidFiles из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1b114-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b114-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1b114-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b114-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1b114-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b114-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b114-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1b114-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1b114-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1b114-133">Введите в поле поиска hello **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="1b114-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="1b114-135">В панели результатов hello выберите **LiquidFiles**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1b114-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b114-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b114-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b114-138">В этом разделе описана настройка и проверка единого входа Azure AD в LiquidFiles с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b114-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b114-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LiquidFiles является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b114-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="1b114-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в LiquidFiles должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1b114-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="1b114-141">В LiquidFiles, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1b114-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b114-142">tooconfigure и теста Azure AD единого входа с LiquidFiles, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1b114-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b114-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1b114-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b114-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1b114-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b114-145">**[Создание тестового пользователя LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave аналог Саймон Britta в LiquidFiles, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b114-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b114-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1b114-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b114-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1b114-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b114-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b114-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b114-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="1b114-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="1b114-150">**tooconfigure Azure AD единого входа с LiquidFiles, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1b114-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b114-151">В hello в hello портала Azure **LiquidFiles** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1b114-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1b114-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1b114-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="1b114-155">На hello **URL-адреса и домена LiquidFiles** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1b114-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="1b114-157">а.</span><span class="sxs-lookup"><span data-stu-id="1b114-157">a.</span></span> <span data-ttu-id="1b114-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="1b114-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="1b114-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b114-159">b.</span></span> <span data-ttu-id="1b114-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="1b114-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="1b114-161">c.</span><span class="sxs-lookup"><span data-stu-id="1b114-161">c.</span></span> <span data-ttu-id="1b114-162">b.</span><span class="sxs-lookup"><span data-stu-id="1b114-162">b.</span></span> <span data-ttu-id="1b114-163">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="1b114-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b114-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="1b114-164">These values are not real.</span></span> <span data-ttu-id="1b114-165">Обновление, эти значения с hello фактический URL-адрес входа, идентификатор и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="1b114-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="1b114-166">Обратитесь к [группа поддержки клиента LiquidFiles](https://www.liquidfiles.com/support.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="1b114-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="1b114-167">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="1b114-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="1b114-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1b114-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1b114-171">На hello **конфигурации LiquidFiles** щелкните **Настройка LiquidFiles** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1b114-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1b114-172">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1b114-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="1b114-174">Корпоративный сайт LiquidFiles tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="1b114-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="1b114-175">Нажмите кнопку **Single Sign-On** в hello **администрирования > конфигурации** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="1b114-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="1b114-176">На hello **настройки единого входа** выполните следующие шаги hello</span><span class="sxs-lookup"><span data-stu-id="1b114-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="1b114-178">а.</span><span class="sxs-lookup"><span data-stu-id="1b114-178">a.</span></span> <span data-ttu-id="1b114-179">Для параметра **Single Sign On Method** (Метод единого входа) выберите значение **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="1b114-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="1b114-180">b.</span><span class="sxs-lookup"><span data-stu-id="1b114-180">b.</span></span> <span data-ttu-id="1b114-181">В hello **URL-адрес входа поставщика Удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1b114-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1b114-182">c.</span><span class="sxs-lookup"><span data-stu-id="1b114-182">c.</span></span> <span data-ttu-id="1b114-183">В hello **URL-адрес выхода поставщика Удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1b114-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1b114-184">d.</span><span class="sxs-lookup"><span data-stu-id="1b114-184">d.</span></span> <span data-ttu-id="1b114-185">В hello **отпечаток сертификата поставщика Удостоверений** текстовое поле, вставить hello **ОТПЕЧАТОК** значение, которое было скопировано из портала Azure...</span><span class="sxs-lookup"><span data-stu-id="1b114-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="1b114-186">д.</span><span class="sxs-lookup"><span data-stu-id="1b114-186">e.</span></span> <span data-ttu-id="1b114-187">Введите в текстовое поле hello формат идентификатора имени значение hello **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="1b114-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="1b114-188">f.</span><span class="sxs-lookup"><span data-stu-id="1b114-188">f.</span></span> <span data-ttu-id="1b114-189">В hello контекста Authn текстовое поле, введите значение hello **urn: oasis: имена: tc: SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="1b114-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="1b114-190">ж.</span><span class="sxs-lookup"><span data-stu-id="1b114-190">g.</span></span> <span data-ttu-id="1b114-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b114-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="1b114-192">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1b114-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b114-193">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1b114-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b114-194">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b114-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b114-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b114-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b114-196">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1b114-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1b114-198">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1b114-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b114-199">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1b114-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b114-201">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1b114-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b114-203">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1b114-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b114-205">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1b114-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b114-207">а.</span><span class="sxs-lookup"><span data-stu-id="1b114-207">a.</span></span> <span data-ttu-id="1b114-208">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b114-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b114-209">b.</span><span class="sxs-lookup"><span data-stu-id="1b114-209">b.</span></span> <span data-ttu-id="1b114-210">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b114-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b114-211">c.</span><span class="sxs-lookup"><span data-stu-id="1b114-211">c.</span></span> <span data-ttu-id="1b114-212">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1b114-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1b114-213">d.</span><span class="sxs-lookup"><span data-stu-id="1b114-213">d.</span></span> <span data-ttu-id="1b114-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b114-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="1b114-215">Создание тестового пользователя LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="1b114-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="1b114-216">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="1b114-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="1b114-217">Работа с вашей tooget администратора сервера LiquidFiles самостоятельно добавить в качестве пользователя перед входом в приложение LiquidFiles tooyour.</span><span class="sxs-lookup"><span data-stu-id="1b114-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1b114-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1b114-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1b114-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLiquidFiles доступа.</span><span class="sxs-lookup"><span data-stu-id="1b114-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1b114-221">**tooassign tooLiquidFiles Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1b114-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b114-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1b114-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1b114-224">В списке приложений hello выберите **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="1b114-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="1b114-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1b114-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1b114-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b114-228">Click **Add** button.</span></span> <span data-ttu-id="1b114-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1b114-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1b114-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1b114-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b114-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1b114-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b114-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1b114-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b114-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1b114-234">Testing single sign-on</span></span>

<span data-ttu-id="1b114-235">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="1b114-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b114-236">При нажатии кнопки LiquidFiles плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour LiquidFiles приложения.</span><span class="sxs-lookup"><span data-stu-id="1b114-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b114-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1b114-237">Additional resources</span></span>

* [<span data-ttu-id="1b114-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b114-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b114-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b114-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

