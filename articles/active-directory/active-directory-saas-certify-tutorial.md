---
title: "Руководство. Интеграция Azure Active Directory с Certify | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и сертификация."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 000bef7b679a6f291b1f3cb42e10cb3ed424b25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="563a0-103">Руководство. Интеграция Azure Active Directory с Certify</span><span class="sxs-lookup"><span data-stu-id="563a0-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="563a0-104">В этом учебнике вы узнаете, как toointegrate сертифицировать Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="563a0-104">In this tutorial, you learn how toointegrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="563a0-105">Интеграция с Azure AD Certify предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="563a0-105">Integrating Certify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="563a0-106">Можно управлять в Azure AD, имеющего доступ tooCertify</span><span class="sxs-lookup"><span data-stu-id="563a0-106">You can control in Azure AD who has access tooCertify</span></span>
- <span data-ttu-id="563a0-107">Можно включить на пользователей tooautomatically get вошедшего tooCertify (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="563a0-107">You can enable your users tooautomatically get signed-on tooCertify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="563a0-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="563a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="563a0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="563a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="563a0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="563a0-110">Prerequisites</span></span>

<span data-ttu-id="563a0-111">Интеграция Azure AD tooconfigure Certify необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="563a0-111">tooconfigure Azure AD integration with Certify, you need hello following items:</span></span>

- <span data-ttu-id="563a0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="563a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="563a0-113">подписка Certify с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="563a0-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="563a0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="563a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="563a0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="563a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="563a0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="563a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="563a0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="563a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="563a0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="563a0-118">Scenario description</span></span>
<span data-ttu-id="563a0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="563a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="563a0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="563a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="563a0-121">Добавление Certify из галереи hello</span><span class="sxs-lookup"><span data-stu-id="563a0-121">Adding Certify from hello gallery</span></span>
2. <span data-ttu-id="563a0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="563a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-hello-gallery"></a><span data-ttu-id="563a0-123">Добавление Certify из галереи hello</span><span class="sxs-lookup"><span data-stu-id="563a0-123">Adding Certify from hello gallery</span></span>
<span data-ttu-id="563a0-124">tooconfigure hello интеграции Certify в Azure AD, вы должны tooadd Certify из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="563a0-124">tooconfigure hello integration of Certify into Azure AD, you need tooadd Certify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="563a0-125">**tooadd Certify из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="563a0-125">**tooadd Certify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="563a0-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="563a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="563a0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="563a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="563a0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="563a0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="563a0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="563a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="563a0-133">Введите в поле поиска hello **Certify**.</span><span class="sxs-lookup"><span data-stu-id="563a0-133">In hello search box, type **Certify**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="563a0-135">В панели результатов hello выберите **Certify**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="563a0-135">In hello results panel, select **Certify**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="563a0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="563a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="563a0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Certify с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="563a0-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="563a0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Certify является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="563a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Certify is tooa user in Azure AD.</span></span> <span data-ttu-id="563a0-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Certify должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="563a0-140">In other words, a link relationship between an Azure AD user and hello related user in Certify needs toobe established.</span></span>

<span data-ttu-id="563a0-141">В Certify, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="563a0-141">In Certify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="563a0-142">tooconfigure и Azure AD тестирования единого входа с Certify требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="563a0-142">tooconfigure and test Azure AD single sign-on with Certify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="563a0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="563a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="563a0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="563a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="563a0-145">**[Создание тестового пользователя Certify](#creating-a-certify-test-user) ** -toohave аналог Саймон Britta в Certify, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="563a0-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - toohave a counterpart of Britta Simon in Certify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="563a0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="563a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="563a0-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="563a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="563a0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="563a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="563a0-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Certify.</span><span class="sxs-lookup"><span data-stu-id="563a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="563a0-150">**tooconfigure Azure AD единого входа с Certify, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="563a0-150">**tooconfigure Azure AD single sign-on with Certify, perform hello following steps:**</span></span>

1. <span data-ttu-id="563a0-151">В hello в hello портала Azure **Certify** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="563a0-151">In hello Azure portal, on hello **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="563a0-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="563a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="563a0-155">На hello **URL-адреса и сертификация домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="563a0-155">On hello **Certify Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="563a0-157">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="563a0-157">In hello **Identifier** textbox, type hello URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="563a0-158">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="563a0-158">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="563a0-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="563a0-160">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="563a0-162">На hello **сертифицировать конфигурации** щелкните **Настройка сертифицировать** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="563a0-162">On hello **Certify Configuration** section, click **Configure Certify** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="563a0-163">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="563a0-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="563a0-165">tooconfigure единого входа на **Certify** стороны, необходимо загрузить hello toosend **Certificate(Raw)** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы**слишком[Certify поддержки](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="563a0-165">tooconfigure single sign-on on **Certify** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="563a0-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="563a0-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="563a0-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="563a0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="563a0-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="563a0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="563a0-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="563a0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="563a0-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="563a0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="563a0-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="563a0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="563a0-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="563a0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="563a0-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="563a0-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="563a0-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="563a0-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="563a0-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="563a0-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="563a0-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="563a0-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="563a0-182">а.</span><span class="sxs-lookup"><span data-stu-id="563a0-182">a.</span></span> <span data-ttu-id="563a0-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="563a0-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="563a0-184">b.</span><span class="sxs-lookup"><span data-stu-id="563a0-184">b.</span></span> <span data-ttu-id="563a0-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="563a0-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="563a0-186">c.</span><span class="sxs-lookup"><span data-stu-id="563a0-186">c.</span></span> <span data-ttu-id="563a0-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="563a0-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="563a0-188">d.</span><span class="sxs-lookup"><span data-stu-id="563a0-188">d.</span></span> <span data-ttu-id="563a0-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="563a0-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="563a0-190">Создание тестового пользователя Certify</span><span class="sxs-lookup"><span data-stu-id="563a0-190">Creating a Certify test user</span></span>

<span data-ttu-id="563a0-191">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Certify.</span><span class="sxs-lookup"><span data-stu-id="563a0-191">hello objective of this section is toocreate a user called Britta Simon in Certify.</span></span> <span data-ttu-id="563a0-192">Приложение Certify поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="563a0-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="563a0-193">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="563a0-193">There is no action item for you in this section.</span></span> <span data-ttu-id="563a0-194">Если он еще не существует во время попытки tooaccess Certify создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="563a0-194">A new user will be created during an attempt tooaccess Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="563a0-195">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Certify поддержки](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="563a0-195">If you need toocreate an user manually, you need toocontact hello [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="563a0-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="563a0-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="563a0-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCertify доступа.</span><span class="sxs-lookup"><span data-stu-id="563a0-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCertify.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="563a0-199">**tooassign tooCertify Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="563a0-199">**tooassign Britta Simon tooCertify, perform hello following steps:**</span></span>

1. <span data-ttu-id="563a0-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="563a0-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="563a0-202">В списке приложений hello выберите **Certify**.</span><span class="sxs-lookup"><span data-stu-id="563a0-202">In hello applications list, select **Certify**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="563a0-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="563a0-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="563a0-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="563a0-206">Click **Add** button.</span></span> <span data-ttu-id="563a0-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="563a0-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="563a0-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="563a0-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="563a0-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="563a0-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="563a0-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="563a0-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="563a0-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="563a0-212">Testing single sign-on</span></span>

<span data-ttu-id="563a0-213">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="563a0-213">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="563a0-214">При нажатии кнопки hello Certify плитки в панели доступа hello, вы должны получить tooyour автоматически вошедшего сертификация приложения.</span><span class="sxs-lookup"><span data-stu-id="563a0-214">When you click hello Certify tile in hello Access Panel, you should get automatically signed-on tooyour Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="563a0-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="563a0-215">Additional resources</span></span>

* [<span data-ttu-id="563a0-216">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="563a0-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="563a0-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="563a0-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

