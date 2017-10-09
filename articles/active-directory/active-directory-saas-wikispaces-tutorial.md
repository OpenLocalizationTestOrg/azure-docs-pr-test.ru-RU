---
title: "Руководство по интеграции Azure Active Directory с Wikispaces | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="61f3c-103">Руководство. Интеграция Azure Active Directory с Wikispaces</span><span class="sxs-lookup"><span data-stu-id="61f3c-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="61f3c-104">В этом учебнике вы узнаете, как toointegrate Wikispaces с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61f3c-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61f3c-105">Интеграция Wikispaces с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="61f3c-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="61f3c-106">Можно управлять в Azure AD, имеющего доступ tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="61f3c-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="61f3c-107">Можно включить на пользователей tooautomatically get вошедшего tooWikispaces (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="61f3c-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61f3c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="61f3c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="61f3c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61f3c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61f3c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="61f3c-110">Prerequisites</span></span>

<span data-ttu-id="61f3c-111">tooconfigure интеграция Azure AD с Wikispaces, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="61f3c-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="61f3c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="61f3c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61f3c-113">Подписка Wikispaces с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="61f3c-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61f3c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="61f3c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61f3c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="61f3c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61f3c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="61f3c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61f3c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61f3c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61f3c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="61f3c-118">Scenario description</span></span>
<span data-ttu-id="61f3c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="61f3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61f3c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="61f3c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61f3c-121">Добавление Wikispaces из галереи hello</span><span class="sxs-lookup"><span data-stu-id="61f3c-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="61f3c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="61f3c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="61f3c-123">Добавление Wikispaces из галереи hello</span><span class="sxs-lookup"><span data-stu-id="61f3c-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="61f3c-124">tooconfigure hello интеграции Wikispaces в Azure AD, вы должны tooadd Wikispaces из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="61f3c-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="61f3c-125">**tooadd Wikispaces из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="61f3c-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="61f3c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="61f3c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="61f3c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="61f3c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="61f3c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="61f3c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="61f3c-133">Введите в поле поиска hello **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-133">In hello search box, type **Wikispaces**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="61f3c-135">В панели результатов hello выберите **Wikispaces**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="61f3c-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61f3c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="61f3c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61f3c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Wikispaces с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61f3c-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61f3c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Wikispaces является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61f3c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="61f3c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Wikispaces должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="61f3c-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="61f3c-141">В Wikispaces, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="61f3c-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="61f3c-142">tooconfigure и теста Azure AD единого входа с Wikispaces, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="61f3c-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="61f3c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="61f3c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="61f3c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="61f3c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61f3c-145">**[Создание тестового пользователя Wikispaces](#creating-a-wikispaces-test-user)**  -toohave аналог Саймон Britta в Wikispaces, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="61f3c-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="61f3c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="61f3c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61f3c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="61f3c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61f3c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="61f3c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61f3c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="61f3c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="61f3c-150">**Azure AD tooconfigure единого входа с Wikispaces, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="61f3c-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="61f3c-151">В hello в hello портала Azure **Wikispaces** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="61f3c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="61f3c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="61f3c-155">На hello **URL-адреса и домена Wikispaces** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="61f3c-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="61f3c-157">а.</span><span class="sxs-lookup"><span data-stu-id="61f3c-157">a.</span></span> <span data-ttu-id="61f3c-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="61f3c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="61f3c-159">b.</span><span class="sxs-lookup"><span data-stu-id="61f3c-159">b.</span></span> <span data-ttu-id="61f3c-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="61f3c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61f3c-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="61f3c-161">These values are not real.</span></span> <span data-ttu-id="61f3c-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="61f3c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="61f3c-163">Обратитесь к [группа поддержки Wikispaces клиента](https://www.wikispaces.com/site/help) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="61f3c-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="61f3c-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="61f3c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="61f3c-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="61f3c-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61f3c-168">tooconfigure единого входа на **Wikispaces** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группой поддержки Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="61f3c-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="61f3c-169">Сразу после завершения настройки hello, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="61f3c-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="61f3c-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="61f3c-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="61f3c-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="61f3c-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="61f3c-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61f3c-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61f3c-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="61f3c-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="61f3c-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="61f3c-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="61f3c-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="61f3c-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="61f3c-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="61f3c-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61f3c-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61f3c-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="61f3c-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61f3c-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="61f3c-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61f3c-185">а.</span><span class="sxs-lookup"><span data-stu-id="61f3c-185">a.</span></span> <span data-ttu-id="61f3c-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61f3c-187">b.</span><span class="sxs-lookup"><span data-stu-id="61f3c-187">b.</span></span> <span data-ttu-id="61f3c-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61f3c-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61f3c-189">c.</span><span class="sxs-lookup"><span data-stu-id="61f3c-189">c.</span></span> <span data-ttu-id="61f3c-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="61f3c-191">d.</span><span class="sxs-lookup"><span data-stu-id="61f3c-191">d.</span></span> <span data-ttu-id="61f3c-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="61f3c-193">Создание тестового пользователя Wikispaces</span><span class="sxs-lookup"><span data-stu-id="61f3c-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="61f3c-194">В порядке tooenable toolog пользователей Azure AD в tooWikispaces их необходимо подготовить в Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="61f3c-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="61f3c-195">В случае hello объекта Wikispaces Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="61f3c-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="61f3c-196">tooprovision учетных записей пользователей, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="61f3c-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="61f3c-197">Войдите в tooyour **Wikispaces** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="61f3c-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="61f3c-198">Go слишком**элементы**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="61f3c-199">![Участники](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Участники")</span><span class="sxs-lookup"><span data-stu-id="61f3c-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="61f3c-200">Нажмите кнопку hello **пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="61f3c-201">![Приглашение участников](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="61f3c-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="61f3c-202">В hello **пригласить пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="61f3c-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="61f3c-203">![Приглашение участников](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="61f3c-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="61f3c-204">а.</span><span class="sxs-lookup"><span data-stu-id="61f3c-204">a.</span></span> <span data-ttu-id="61f3c-205">Тип hello **имена пользователей или адреса электронной почты** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="61f3c-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="61f3c-206">b.</span><span class="sxs-lookup"><span data-stu-id="61f3c-206">b.</span></span> <span data-ttu-id="61f3c-207">Нажмите кнопку **Send**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="61f3c-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="61f3c-208">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="61f3c-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="61f3c-209">Можно использовать любые другие Wikispaces пользователя средства создания учетных записей или интерфейсы API, предоставляемые Wikispaces tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="61f3c-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="61f3c-210">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="61f3c-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="61f3c-211">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWikispaces доступа.</span><span class="sxs-lookup"><span data-stu-id="61f3c-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="61f3c-213">**tooassign tooWikispaces Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="61f3c-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="61f3c-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="61f3c-216">В списке приложений hello выберите **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="61f3c-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="61f3c-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-220">Click **Add** button.</span></span> <span data-ttu-id="61f3c-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="61f3c-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="61f3c-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="61f3c-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61f3c-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="61f3c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61f3c-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="61f3c-226">Testing single sign-on</span></span>

<span data-ttu-id="61f3c-227">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="61f3c-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="61f3c-228">При нажатии кнопки Wikispaces плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в Wikispaces приложения.</span><span class="sxs-lookup"><span data-stu-id="61f3c-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="61f3c-229">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61f3c-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61f3c-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="61f3c-230">Additional resources</span></span>

* [<span data-ttu-id="61f3c-231">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61f3c-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61f3c-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61f3c-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

