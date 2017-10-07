---
title: "Руководство по интеграции Azure Active Directory с PostBeyond | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PostBeyond."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 38019fd24a603732e91a1b5f7bfed5ab4edb017f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="d525e-103">Руководство. Интеграция Azure Active Directory с PostBeyond</span><span class="sxs-lookup"><span data-stu-id="d525e-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="d525e-104">В этом учебнике вы узнаете, как toointegrate PostBeyond с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d525e-104">In this tutorial, you learn how toointegrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d525e-105">Интеграция с Azure AD PostBeyond предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d525e-105">Integrating PostBeyond with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d525e-106">Можно управлять в Azure AD, имеющего доступ tooPostBeyond</span><span class="sxs-lookup"><span data-stu-id="d525e-106">You can control in Azure AD who has access tooPostBeyond</span></span>
- <span data-ttu-id="d525e-107">Можно включить на пользователей tooautomatically get вошедшего tooPostBeyond (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d525e-107">You can enable your users tooautomatically get signed-on tooPostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d525e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d525e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d525e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d525e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d525e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d525e-110">Prerequisites</span></span>

<span data-ttu-id="d525e-111">tooconfigure интеграция Azure AD с PostBeyond требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d525e-111">tooconfigure Azure AD integration with PostBeyond, you need hello following items:</span></span>

- <span data-ttu-id="d525e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d525e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d525e-113">подписка PostBeyond с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d525e-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d525e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d525e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d525e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d525e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d525e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d525e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d525e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d525e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d525e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d525e-118">Scenario description</span></span>
<span data-ttu-id="d525e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d525e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d525e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d525e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d525e-121">Добавление PostBeyond из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d525e-121">Adding PostBeyond from hello gallery</span></span>
2. <span data-ttu-id="d525e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d525e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-hello-gallery"></a><span data-ttu-id="d525e-123">Добавление PostBeyond из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d525e-123">Adding PostBeyond from hello gallery</span></span>
<span data-ttu-id="d525e-124">интеграции hello tooconfigure PostBeyond в Azure AD, вы должны tooadd PostBeyond из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d525e-124">tooconfigure hello integration of PostBeyond into Azure AD, you need tooadd PostBeyond from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d525e-125">**tooadd PostBeyond из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d525e-125">**tooadd PostBeyond from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d525e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d525e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d525e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d525e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d525e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d525e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d525e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d525e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d525e-133">Введите в поле поиска hello **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="d525e-133">In hello search box, type **PostBeyond**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="d525e-135">В панели результатов hello выберите **PostBeyond**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d525e-135">In hello results panel, select **PostBeyond**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d525e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d525e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d525e-138">В этом разделе описана настройка и проверка единого входа Azure AD в PostBeyond с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d525e-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d525e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PostBeyond является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d525e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PostBeyond is tooa user in Azure AD.</span></span> <span data-ttu-id="d525e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в PostBeyond должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d525e-140">In other words, a link relationship between an Azure AD user and hello related user in PostBeyond needs toobe established.</span></span>

<span data-ttu-id="d525e-141">В PostBeyond, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d525e-141">In PostBeyond, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d525e-142">tooconfigure и теста Azure AD единого входа с PostBeyond, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d525e-142">tooconfigure and test Azure AD single sign-on with PostBeyond, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d525e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d525e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d525e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d525e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d525e-145">**[Создание PostBeyond тестового пользователя](#creating-a-postbeyond-test-user)**  -toohave аналог Саймон Britta в PostBeyond, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d525e-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - toohave a counterpart of Britta Simon in PostBeyond that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d525e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d525e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d525e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d525e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d525e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d525e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d525e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="d525e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="d525e-150">**tooconfigure Azure AD единого входа с PostBeyond, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d525e-150">**tooconfigure Azure AD single sign-on with PostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="d525e-151">В hello в hello портала Azure **PostBeyond** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d525e-151">In hello Azure portal, on hello **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d525e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d525e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="d525e-155">На hello **URL-адреса и домена PostBeyond** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d525e-155">On hello **PostBeyond Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="d525e-157">а.</span><span class="sxs-lookup"><span data-stu-id="d525e-157">a.</span></span> <span data-ttu-id="d525e-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="d525e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="d525e-159">b.</span><span class="sxs-lookup"><span data-stu-id="d525e-159">b.</span></span> <span data-ttu-id="d525e-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="d525e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d525e-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d525e-161">These values are not real.</span></span> <span data-ttu-id="d525e-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d525e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d525e-163">Обратитесь к [группа поддержки клиента PostBeyond](mailto:sso@postbeyond.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="d525e-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="d525e-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d525e-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="d525e-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d525e-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d525e-168">На hello **конфигурации PostBeyond** щелкните **Настройка PostBeyond** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d525e-168">On hello **PostBeyond Configuration** section, click **Configure PostBeyond** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d525e-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="d525e-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="d525e-171">tooconfigure единого входа на **PostBeyond** стороны, необходимо загрузить hello toosend **Certificate(Base64)**, **идентификатор сущности SAML**, **SAML Single Sign-On URL-адрес службы** и **URL-адрес выхода** слишком[PostBeyond поддержки](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="d525e-171">tooconfigure single sign-on on **PostBeyond** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** too[PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="d525e-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="d525e-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d525e-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d525e-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d525e-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d525e-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d525e-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d525e-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d525e-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d525e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d525e-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d525e-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d525e-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d525e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d525e-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d525e-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d525e-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d525e-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d525e-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d525e-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d525e-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d525e-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d525e-188">а.</span><span class="sxs-lookup"><span data-stu-id="d525e-188">a.</span></span> <span data-ttu-id="d525e-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d525e-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d525e-190">b.</span><span class="sxs-lookup"><span data-stu-id="d525e-190">b.</span></span> <span data-ttu-id="d525e-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d525e-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d525e-192">c.</span><span class="sxs-lookup"><span data-stu-id="d525e-192">c.</span></span> <span data-ttu-id="d525e-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d525e-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d525e-194">d.</span><span class="sxs-lookup"><span data-stu-id="d525e-194">d.</span></span> <span data-ttu-id="d525e-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d525e-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="d525e-196">Создание тестового пользователя PostBeyond</span><span class="sxs-lookup"><span data-stu-id="d525e-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="d525e-197">В этом разделе описано, как создать пользователя Britta Simon в приложении PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="d525e-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="d525e-198">Если вы не знаете, как tooadd Britta Simon в PostBeyond, можно работать с [PostBeyond поддержки](mailto:sso@postbeyond.com) tooadd hello тестового пользователя и Включение единого входа.</span><span class="sxs-lookup"><span data-stu-id="d525e-198">If you don't know how tooadd Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d525e-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d525e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d525e-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPostBeyond доступа.</span><span class="sxs-lookup"><span data-stu-id="d525e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPostBeyond.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d525e-202">**tooassign tooPostBeyond Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d525e-202">**tooassign Britta Simon tooPostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="d525e-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d525e-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d525e-205">В списке приложений hello выберите **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="d525e-205">In hello applications list, select **PostBeyond**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="d525e-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d525e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d525e-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d525e-209">Click **Add** button.</span></span> <span data-ttu-id="d525e-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d525e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d525e-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d525e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d525e-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d525e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d525e-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d525e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d525e-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d525e-215">Testing single sign-on</span></span>

<span data-ttu-id="d525e-216">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="d525e-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d525e-217">При нажатии кнопки PostBeyond плитки hello в hello панели доступа, вы должны получить toohello PostBeyond входа на странице.</span><span class="sxs-lookup"><span data-stu-id="d525e-217">When you click hello PostBeyond tile in hello Access Panel, you should get toohello PostBeyond sign in page.</span></span> <span data-ttu-id="d525e-218">Щелкните **Sign in with Office 365**(Вход с использованием Office 365) и введите учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d525e-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="d525e-219">После этого вы должны войти в PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="d525e-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d525e-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d525e-220">Additional resources</span></span>

* [<span data-ttu-id="d525e-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d525e-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d525e-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d525e-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

