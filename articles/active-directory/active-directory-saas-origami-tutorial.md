---
title: "Руководство по интеграции Azure Active Directory с Origami | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Оригами."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="bd776-103">Руководство. Интеграция Azure Active Directory с Origami</span><span class="sxs-lookup"><span data-stu-id="bd776-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="bd776-104">В этом учебнике вы узнаете, как toointegrate оригами с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd776-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd776-105">Интеграция с Azure AD оригами предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bd776-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd776-106">Можно управлять в Azure AD, имеющего доступ tooOrigami</span><span class="sxs-lookup"><span data-stu-id="bd776-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="bd776-107">Можно включить на пользователей tooautomatically get вошедшего tooOrigami (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd776-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd776-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bd776-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd776-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd776-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd776-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bd776-110">Prerequisites</span></span>

<span data-ttu-id="bd776-111">tooconfigure интеграция Azure AD с оригами требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bd776-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="bd776-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bd776-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd776-113">подписка Origami с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bd776-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd776-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bd776-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd776-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bd776-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd776-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bd776-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd776-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd776-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd776-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bd776-118">Scenario description</span></span>
<span data-ttu-id="bd776-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bd776-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd776-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bd776-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd776-121">Добавление оригами из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bd776-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="bd776-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd776-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="bd776-123">Добавление оригами из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bd776-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="bd776-124">tooconfigure hello интеграции оригами в Azure AD, вы должны tooadd оригами из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bd776-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd776-125">**tooadd оригами из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bd776-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd776-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bd776-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd776-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bd776-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd776-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bd776-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bd776-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bd776-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bd776-133">Введите в поле поиска hello **оригами**.</span><span class="sxs-lookup"><span data-stu-id="bd776-133">In hello search box, type **Origami**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="bd776-135">В панели результатов hello выберите **оригами**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd776-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd776-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd776-138">В этом разделе описана настройка и проверка единого входа Azure AD в Origami с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bd776-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bd776-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в оригами является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd776-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="bd776-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в оригами должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bd776-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="bd776-141">В оригами, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="bd776-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd776-142">tooconfigure и теста Azure AD единого входа с оригами, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bd776-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd776-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bd776-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd776-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bd776-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd776-145">**[Создание тестового пользователя, прошедшего оригами](#creating-an-origami-test-user)**  -toohave аналог Саймон Britta в оригами, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd776-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd776-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bd776-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd776-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bd776-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd776-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd776-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd776-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Оригами.</span><span class="sxs-lookup"><span data-stu-id="bd776-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="bd776-150">**tooconfigure Azure AD единого входа с оригами, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bd776-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd776-151">В hello в hello портала Azure **оригами** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bd776-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bd776-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bd776-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="bd776-155">На hello **URL-адреса и домена оригами** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bd776-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="bd776-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bd776-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd776-158">значение Hello не является вещественным числом.</span><span class="sxs-lookup"><span data-stu-id="bd776-158">hello value is not real.</span></span> <span data-ttu-id="bd776-159">Значение hello обновления с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="bd776-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bd776-160">Обратитесь к [группа поддержки клиента оригами](https://wordpress.org/support/theme/origami) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="bd776-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="bd776-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="bd776-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bd776-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd776-165">На hello **конфигурации оригами** щелкните **Настройка оригами** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="bd776-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bd776-166">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="bd776-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="bd776-168">Войдите в toohello оригами учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bd776-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="bd776-169">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="bd776-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="bd776-171">На странице диалогового окна hello единого входа в программу установки выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="bd776-173">а.</span><span class="sxs-lookup"><span data-stu-id="bd776-173">a.</span></span> <span data-ttu-id="bd776-174">Выберите пункт **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bd776-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="bd776-175">b.</span><span class="sxs-lookup"><span data-stu-id="bd776-175">b.</span></span> <span data-ttu-id="bd776-176">В hello **поставщика удостоверений вход URL-адрес страницы** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bd776-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bd776-177">c.</span><span class="sxs-lookup"><span data-stu-id="bd776-177">c.</span></span> <span data-ttu-id="bd776-178">В hello **URL-адрес страницы выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bd776-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bd776-179">d.</span><span class="sxs-lookup"><span data-stu-id="bd776-179">d.</span></span> <span data-ttu-id="bd776-180">Нажмите кнопку **Обзор** tooupload hello сертификат, загруженный с портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="bd776-181">д.</span><span class="sxs-lookup"><span data-stu-id="bd776-181">e.</span></span> <span data-ttu-id="bd776-182">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="bd776-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bd776-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bd776-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd776-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd776-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd776-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd776-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd776-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd776-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bd776-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bd776-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bd776-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd776-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bd776-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd776-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bd776-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd776-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bd776-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd776-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bd776-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd776-198">а.</span><span class="sxs-lookup"><span data-stu-id="bd776-198">a.</span></span> <span data-ttu-id="bd776-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd776-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd776-200">b.</span><span class="sxs-lookup"><span data-stu-id="bd776-200">b.</span></span> <span data-ttu-id="bd776-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd776-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd776-202">c.</span><span class="sxs-lookup"><span data-stu-id="bd776-202">c.</span></span> <span data-ttu-id="bd776-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bd776-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd776-204">d.</span><span class="sxs-lookup"><span data-stu-id="bd776-204">d.</span></span> <span data-ttu-id="bd776-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bd776-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="bd776-206">Создание тестового пользователя Origami</span><span class="sxs-lookup"><span data-stu-id="bd776-206">Creating an Origami test user</span></span>

<span data-ttu-id="bd776-207">В этом разделе описано, как создать пользователя Britta Simon в приложении Origami.</span><span class="sxs-lookup"><span data-stu-id="bd776-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="bd776-208">Войдите в toohello оригами учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="bd776-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="bd776-209">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="bd776-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="bd776-211">На hello **пользователей и безопасности** диалоговое окно, нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bd776-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="bd776-213">Нажмите кнопку **Add New User**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="bd776-213">Click **Add New User**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="bd776-215">В диалоговом окне Добавить пользователя hello выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="bd776-217">а.</span><span class="sxs-lookup"><span data-stu-id="bd776-217">a.</span></span> <span data-ttu-id="bd776-218">В hello **имя пользователя** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="bd776-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="bd776-219">b.</span><span class="sxs-lookup"><span data-stu-id="bd776-219">b.</span></span> <span data-ttu-id="bd776-220">В hello **пароль** введите пароль.</span><span class="sxs-lookup"><span data-stu-id="bd776-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="bd776-221">c.</span><span class="sxs-lookup"><span data-stu-id="bd776-221">c.</span></span> <span data-ttu-id="bd776-222">В hello **подтверждение пароля** textbox hello введите пароль еще раз.</span><span class="sxs-lookup"><span data-stu-id="bd776-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="bd776-223">d.</span><span class="sxs-lookup"><span data-stu-id="bd776-223">d.</span></span> <span data-ttu-id="bd776-224">В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bd776-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="bd776-225">д.</span><span class="sxs-lookup"><span data-stu-id="bd776-225">e.</span></span> <span data-ttu-id="bd776-226">В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bd776-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="bd776-227">f.</span><span class="sxs-lookup"><span data-stu-id="bd776-227">f.</span></span> <span data-ttu-id="bd776-228">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bd776-228">Click **Save**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="bd776-230">Назначьте **роли пользователей** и **клиентского доступа** toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd776-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd776-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bd776-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd776-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOrigami доступа.</span><span class="sxs-lookup"><span data-stu-id="bd776-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bd776-235">**tooassign tooOrigami Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bd776-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd776-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bd776-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bd776-238">В списке приложений hello выберите **оригами**.</span><span class="sxs-lookup"><span data-stu-id="bd776-238">In hello applications list, select **Origami**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="bd776-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bd776-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bd776-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bd776-242">Click **Add** button.</span></span> <span data-ttu-id="bd776-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bd776-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bd776-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd776-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bd776-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd776-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bd776-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd776-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bd776-248">Testing single sign-on</span></span>

<span data-ttu-id="bd776-249">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bd776-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd776-250">При выборе плитки оригами hello в hello панели доступа, следует получать автоматически вошедшего tooyour оригами приложения.</span><span class="sxs-lookup"><span data-stu-id="bd776-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd776-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bd776-251">Additional resources</span></span>

* [<span data-ttu-id="bd776-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd776-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd776-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd776-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

