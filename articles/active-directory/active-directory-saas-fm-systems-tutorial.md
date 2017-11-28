---
title: "Руководство по интеграции Azure Active Directory с FM:Systems | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FM: Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="18606-103">Руководство по интеграции Azure Active Directory с FM:Systems</span><span class="sxs-lookup"><span data-stu-id="18606-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="18606-104">В этом учебнике вы узнаете, как toointegrate FM: Systems с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18606-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18606-105">Интеграция FM: Systems с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="18606-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18606-106">Можно управлять в Azure AD, имеющего доступ tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="18606-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="18606-107">Можно включить на пользователей tooautomatically get вошедшего tooFM:Systems (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="18606-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18606-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="18606-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18606-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18606-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18606-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18606-110">Prerequisites</span></span>

<span data-ttu-id="18606-111">tooconfigure интеграция Azure AD с FM: Systems, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="18606-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="18606-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="18606-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18606-113">подписка FM:Systems с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="18606-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18606-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="18606-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18606-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="18606-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18606-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="18606-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18606-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18606-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18606-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="18606-118">Scenario description</span></span>
<span data-ttu-id="18606-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="18606-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18606-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="18606-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18606-121">Добавление FM: Systems из галереи hello</span><span class="sxs-lookup"><span data-stu-id="18606-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="18606-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18606-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="18606-123">Добавление FM: Systems из галереи hello</span><span class="sxs-lookup"><span data-stu-id="18606-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="18606-124">tooconfigure hello интеграции FM: Systems в Azure AD, вы должны tooadd FM: Systems из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="18606-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18606-125">**tooadd FM: Systems из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="18606-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18606-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="18606-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18606-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="18606-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18606-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18606-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="18606-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="18606-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="18606-133">Введите в поле поиска hello **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="18606-133">In hello search box, type **FM:Systems**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="18606-135">В панели результатов hello выберите **FM: Systems**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="18606-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18606-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18606-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18606-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FM:Systems для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="18606-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18606-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FM: Systems является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18606-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="18606-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в FM: Systems должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="18606-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="18606-141">В FM: Systems, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="18606-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18606-142">tooconfigure и теста Azure AD единого входа с FM: Systems, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="18606-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18606-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="18606-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18606-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="18606-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18606-145">**[Создание тестового пользователя FM: Systems](#creating-an-fmsystems-test-user)**  -toohave аналог Саймон Britta в FM: Systems, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="18606-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18606-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="18606-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18606-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="18606-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18606-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="18606-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18606-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении FM: Systems.</span><span class="sxs-lookup"><span data-stu-id="18606-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="18606-150">**Azure AD tooconfigure единого входа с FM: Systems, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="18606-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="18606-151">В hello в hello портала Azure **FM: Systems** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="18606-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="18606-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="18606-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="18606-155">На hello **URL-адреса и домена FM: Systems** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="18606-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="18606-157">В hello **URL-адрес ответа** текстовом поле введите FM: Systems **URL-адрес ответа**, hello введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="18606-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18606-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="18606-158">This value is not real.</span></span> <span data-ttu-id="18606-159">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="18606-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="18606-160">Обратитесь к [группа поддержки FM: Systems](https://fmsystems.com/ask-us/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="18606-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="18606-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="18606-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="18606-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="18606-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18606-165">tooconfigure единого входа на **FM: Systems** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки FM: Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="18606-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="18606-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="18606-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="18606-167">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="18606-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="18606-168">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="18606-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18606-169">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="18606-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18606-170">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18606-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18606-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="18606-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="18606-172">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="18606-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="18606-174">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="18606-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18606-175">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="18606-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18606-177">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="18606-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18606-179">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="18606-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18606-181">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="18606-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18606-183">а.</span><span class="sxs-lookup"><span data-stu-id="18606-183">a.</span></span> <span data-ttu-id="18606-184">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18606-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18606-185">b.</span><span class="sxs-lookup"><span data-stu-id="18606-185">b.</span></span> <span data-ttu-id="18606-186">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18606-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18606-187">c.</span><span class="sxs-lookup"><span data-stu-id="18606-187">c.</span></span> <span data-ttu-id="18606-188">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="18606-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18606-189">d.</span><span class="sxs-lookup"><span data-stu-id="18606-189">d.</span></span> <span data-ttu-id="18606-190">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="18606-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="18606-191">Создание тестового пользователя FM:Systems</span><span class="sxs-lookup"><span data-stu-id="18606-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="18606-192">В другом окне веб-браузера войдите на ваш корпоративный веб-сайт FM: Systems в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="18606-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="18606-193">Go слишком**системное администрирование \> Управление безопасностью \> пользователей \> список пользователей**.</span><span class="sxs-lookup"><span data-stu-id="18606-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="18606-194">![Администрирование системы](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Администрирование системы")</span><span class="sxs-lookup"><span data-stu-id="18606-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="18606-195">Нажмите **Создать нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="18606-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="18606-196">![Создание пользователя](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="18606-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="18606-197">В hello **Create User** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="18606-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="18606-198">![Создание пользователя](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="18606-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="18606-199">а.</span><span class="sxs-lookup"><span data-stu-id="18606-199">a.</span></span> <span data-ttu-id="18606-200">Тип hello **UserName**, hello **пароль**, **подтверждение пароля**, **электронной почты** и hello **идентификатор сотрудника**из допустимых Azure связанные с учетной записью Active Directory требуется tooprovision в hello текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="18606-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="18606-201">b.</span><span class="sxs-lookup"><span data-stu-id="18606-201">b.</span></span> <span data-ttu-id="18606-202">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="18606-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18606-203">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="18606-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18606-204">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFM:Systems доступа.</span><span class="sxs-lookup"><span data-stu-id="18606-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="18606-206">**tooassign tooFM:Systems Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="18606-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="18606-207">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="18606-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="18606-209">В списке приложений hello выберите **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="18606-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="18606-211">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="18606-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="18606-213">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="18606-213">Click **Add** button.</span></span> <span data-ttu-id="18606-214">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="18606-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="18606-216">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="18606-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18606-217">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="18606-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18606-218">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="18606-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18606-219">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="18606-219">Testing single sign-on</span></span>

<span data-ttu-id="18606-220">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="18606-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18606-221">При выборе плитки FM: Systems hello в hello панели доступа, вы должны получить приложение автоматически вошедшего tooyour FM: Systems.</span><span class="sxs-lookup"><span data-stu-id="18606-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="18606-222">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18606-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18606-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="18606-223">Additional resources</span></span>

* [<span data-ttu-id="18606-224">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18606-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18606-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18606-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

