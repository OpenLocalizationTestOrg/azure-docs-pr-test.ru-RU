---
title: "Руководство по интеграции Azure Active Directory с Projectplace | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="4fcb8-103">Учебник. Интеграция Azure Active Directory с Projectplace</span><span class="sxs-lookup"><span data-stu-id="4fcb8-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="4fcb8-104">В этом учебнике вы узнаете, как toointegrate Projectplace в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fcb8-105">Интеграция с Azure AD Projectplace предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fcb8-106">Можно управлять в Azure AD, имеющего доступ tooProjectplace</span><span class="sxs-lookup"><span data-stu-id="4fcb8-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="4fcb8-107">Можно включить на пользователей tooautomatically get вошедшего tooProjectplace (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fcb8-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fcb8-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4fcb8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4fcb8-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fcb8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4fcb8-110">Prerequisites</span></span>

<span data-ttu-id="4fcb8-111">tooconfigure интеграция Azure AD с Projectplace требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="4fcb8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4fcb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fcb8-113">подписка Projectplace с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fcb8-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fcb8-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fcb8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fcb8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fcb8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4fcb8-118">Scenario description</span></span>
<span data-ttu-id="4fcb8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fcb8-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fcb8-121">Добавление Projectplace из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4fcb8-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="4fcb8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fcb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="4fcb8-123">Добавление Projectplace из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4fcb8-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="4fcb8-124">tooconfigure hello интеграции Projectplace в Azure AD, вы должны tooadd Projectplace из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fcb8-125">**tooadd Projectplace из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4fcb8-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fcb8-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fcb8-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fcb8-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4fcb8-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4fcb8-133">Введите в поле поиска hello **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-133">In hello search box, type **Projectplace**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="4fcb8-135">В панели результатов hello выберите **Projectplace**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fcb8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fcb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fcb8-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Projectplace с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fcb8-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Projectplace является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="4fcb8-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Projectplace должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="4fcb8-141">В Projectplace, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4fcb8-142">tooconfigure и теста Azure AD единого входа с Projectplace, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fcb8-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fcb8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fcb8-145">**[Создание тестового пользователя Projectplace](#creating-a-projectplace-test-user)**  -toohave аналог Саймон Britta в Projectplace, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fcb8-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fcb8-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fcb8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fcb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fcb8-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Projectplace.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="4fcb8-150">**tooconfigure Azure AD единого входа с Projectplace, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4fcb8-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fcb8-151">В hello в hello портала Azure **Projectplace** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4fcb8-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="4fcb8-155">На hello **URL-адреса и домена Projectplace** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="4fcb8-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="4fcb8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fcb8-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-158">This value is not real.</span></span> <span data-ttu-id="4fcb8-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4fcb8-160">Обратитесь к [группа поддержки Projectplace клиента](https://success.planview.com/Projectplace/Support) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="4fcb8-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="4fcb8-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4fcb8-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4fcb8-165">tooconfigure единого входа на **Projectplace** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="4fcb8-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="4fcb8-167">Hello единого входа конфигурация имеет выполненных hello toobe [поддержки projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="4fcb8-168">Сразу после завершения настройки hello, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="4fcb8-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4fcb8-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fcb8-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fcb8-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fcb8-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fcb8-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fcb8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fcb8-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4fcb8-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4fcb8-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fcb8-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fcb8-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fcb8-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4fcb8-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fcb8-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fcb8-184">а.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-184">a.</span></span> <span data-ttu-id="4fcb8-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fcb8-186">b.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-186">b.</span></span> <span data-ttu-id="4fcb8-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fcb8-188">c.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-188">c.</span></span> <span data-ttu-id="4fcb8-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4fcb8-190">d.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-190">d.</span></span> <span data-ttu-id="4fcb8-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="4fcb8-192">Создание тестового пользователя Projectplace</span><span class="sxs-lookup"><span data-stu-id="4fcb8-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="4fcb8-193">В порядке tooenable toolog пользователей Azure AD в Projectplace их необходимо подготовить в Projectplace.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="4fcb8-194">В случае Projectplace hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="4fcb8-195">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4fcb8-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fcb8-196">Войдите в tooyour **Projectplace** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="4fcb8-197">Go слишком**людей**, а затем нажмите кнопку **члены**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="4fcb8-198">![Люди](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="4fcb8-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="4fcb8-199">Щелкните **Добавить участника**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="4fcb8-200">![Добавление участников](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Добавление участников")</span><span class="sxs-lookup"><span data-stu-id="4fcb8-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="4fcb8-201">В hello **Add Member** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4fcb8-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4fcb8-202">![Новые участники](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Новые участники")</span><span class="sxs-lookup"><span data-stu-id="4fcb8-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="4fcb8-203">а.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-203">a.</span></span> <span data-ttu-id="4fcb8-204">В hello **новых членов** текстовом поле введите адрес электронной почты hello действительной учетной записи AAD, которые должны tooprovision hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="4fcb8-205">b.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-205">b.</span></span> <span data-ttu-id="4fcb8-206">Нажмите кнопку **Send**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-206">Click **Send**.</span></span>

   <span data-ttu-id="4fcb8-207">Владелец учетной записи Azure Active Directory toohello отправки одного сообщения, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="4fcb8-208">Можно использовать любые другие Projectplace пользователя средства создания учетных записей или интерфейсы API, предоставляемые Projectplace tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4fcb8-209">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4fcb8-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4fcb8-210">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooProjectplace доступа.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4fcb8-212">**tooassign tooProjectplace Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4fcb8-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fcb8-213">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4fcb8-215">В списке приложений hello выберите **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-215">In hello applications list, select **Projectplace**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="4fcb8-217">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4fcb8-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-219">Click **Add** button.</span></span> <span data-ttu-id="4fcb8-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4fcb8-222">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fcb8-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fcb8-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fcb8-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4fcb8-225">Testing single sign-on</span></span>

<span data-ttu-id="4fcb8-226">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fcb8-227">При нажатии кнопки hello Projectplace плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Projectplace.</span><span class="sxs-lookup"><span data-stu-id="4fcb8-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="4fcb8-228">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fcb8-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fcb8-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4fcb8-229">Additional resources</span></span>

* [<span data-ttu-id="4fcb8-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fcb8-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fcb8-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fcb8-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

