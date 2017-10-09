---
title: "Руководство по интеграции Azure Active Directory с Trakopolis | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 00f9b21c0a837d1d9fbbd9135367fae4b02db934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="ed142-103">Учебник. Интеграция Azure Active Directory с Trakopolis</span><span class="sxs-lookup"><span data-stu-id="ed142-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="ed142-104">В этом учебнике вы узнаете, как toointegrate Trakopolis с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed142-104">In this tutorial, you learn how toointegrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed142-105">Интеграция с Azure AD Trakopolis предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ed142-105">Integrating Trakopolis with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed142-106">Можно управлять в Azure AD, имеющего доступ tooTrakopolis</span><span class="sxs-lookup"><span data-stu-id="ed142-106">You can control in Azure AD who has access tooTrakopolis</span></span>
- <span data-ttu-id="ed142-107">Можно включить на пользователей tooautomatically get вошедшего tooTrakopolis (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed142-107">You can enable your users tooautomatically get signed-on tooTrakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed142-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ed142-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ed142-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed142-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed142-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed142-110">Prerequisites</span></span>

<span data-ttu-id="ed142-111">tooconfigure интеграция Azure AD с Trakopolis требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ed142-111">tooconfigure Azure AD integration with Trakopolis, you need hello following items:</span></span>

- <span data-ttu-id="ed142-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ed142-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed142-113">подписка Trakopolis с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed142-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed142-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ed142-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed142-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ed142-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed142-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ed142-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed142-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed142-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed142-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ed142-118">Scenario description</span></span>
<span data-ttu-id="ed142-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ed142-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed142-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ed142-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed142-121">Добавление Trakopolis из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ed142-121">Adding Trakopolis from hello gallery</span></span>
2. <span data-ttu-id="ed142-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed142-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-hello-gallery"></a><span data-ttu-id="ed142-123">Добавление Trakopolis из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ed142-123">Adding Trakopolis from hello gallery</span></span>
<span data-ttu-id="ed142-124">tooconfigure hello интеграции Trakopolis в Azure AD, вы должны tooadd Trakopolis из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed142-124">tooconfigure hello integration of Trakopolis into Azure AD, you need tooadd Trakopolis from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed142-125">**tooadd Trakopolis из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed142-125">**tooadd Trakopolis from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed142-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ed142-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed142-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ed142-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed142-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed142-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ed142-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ed142-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ed142-133">Введите в поле поиска hello **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="ed142-133">In hello search box, type **Trakopolis**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="ed142-135">В панели результатов hello выберите **Trakopolis**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ed142-135">In hello results panel, select **Trakopolis**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed142-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed142-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed142-138">В этом разделе описана настройка и проверка единого входа Azure AD в Trakopolis с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed142-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed142-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Trakopolis является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed142-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trakopolis is tooa user in Azure AD.</span></span> <span data-ttu-id="ed142-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Trakopolis должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ed142-140">In other words, a link relationship between an Azure AD user and hello related user in Trakopolis needs toobe established.</span></span>

<span data-ttu-id="ed142-141">В Trakopolis, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ed142-141">In Trakopolis, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ed142-142">tooconfigure и теста Azure AD единого входа с Trakopolis, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ed142-142">tooconfigure and test Azure AD single sign-on with Trakopolis, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed142-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ed142-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed142-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ed142-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed142-145">**[Создание тестового пользователя Trakopolis](#creating-a-trakopolis-test-user)**  -toohave аналог Саймон Britta в Trakopolis, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ed142-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - toohave a counterpart of Britta Simon in Trakopolis that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed142-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ed142-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed142-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed142-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed142-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed142-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed142-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ed142-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="ed142-150">**tooconfigure Azure AD единого входа с Trakopolis, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed142-150">**tooconfigure Azure AD single sign-on with Trakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed142-151">В hello в hello портала Azure **Trakopolis** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ed142-151">In hello Azure portal, on hello **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ed142-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed142-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="ed142-155">На hello **URL-адреса и домена Trakopolis** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ed142-155">On hello **Trakopolis Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="ed142-157">а.</span><span class="sxs-lookup"><span data-stu-id="ed142-157">a.</span></span> <span data-ttu-id="ed142-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="ed142-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="ed142-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed142-159">b.</span></span> <span data-ttu-id="ed142-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="ed142-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed142-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ed142-161">These values are not real.</span></span> <span data-ttu-id="ed142-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ed142-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ed142-163">Обратитесь к [группа поддержки клиента Trakopolis](mailto:support@cantelematics.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ed142-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) tooget these values.</span></span> 

4. <span data-ttu-id="ed142-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed142-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="ed142-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ed142-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed142-168">На hello **конфигурации Trakopolis** щелкните **Настройка Trakopolis** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ed142-168">On hello **Trakopolis Configuration** section, click **Configure Trakopolis** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ed142-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ed142-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="ed142-171">tooconfigure единого входа на **Trakopolis** стороны, необходимо загрузить hello toosend **метаданные в формате XML, URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Trakopolis поддержки](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="ed142-171">tooconfigure single sign-on on **Trakopolis** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="ed142-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="ed142-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ed142-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ed142-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed142-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ed142-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed142-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed142-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed142-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed142-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed142-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ed142-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ed142-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed142-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed142-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ed142-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed142-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ed142-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed142-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ed142-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed142-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ed142-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed142-188">а.</span><span class="sxs-lookup"><span data-stu-id="ed142-188">a.</span></span> <span data-ttu-id="ed142-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed142-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed142-190">b.</span><span class="sxs-lookup"><span data-stu-id="ed142-190">b.</span></span> <span data-ttu-id="ed142-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed142-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed142-192">c.</span><span class="sxs-lookup"><span data-stu-id="ed142-192">c.</span></span> <span data-ttu-id="ed142-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ed142-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ed142-194">d.</span><span class="sxs-lookup"><span data-stu-id="ed142-194">d.</span></span> <span data-ttu-id="ed142-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ed142-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="ed142-196">Создание тестового пользователя Trakopolis</span><span class="sxs-lookup"><span data-stu-id="ed142-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="ed142-197">В этом разделе описано, как создать пользователя Britta Simon в Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ed142-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="ed142-198">Работать с [Trakopolis поддержки](mailto:support@cantelematics.com) для добавления пользователей hello в платформе Trakopolis hello.</span><span class="sxs-lookup"><span data-stu-id="ed142-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add hello users in hello Trakopolis platform.</span></span> <span data-ttu-id="ed142-199">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="ed142-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ed142-200">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ed142-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ed142-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTrakopolis доступа.</span><span class="sxs-lookup"><span data-stu-id="ed142-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrakopolis.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ed142-203">**tooassign tooTrakopolis Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed142-203">**tooassign Britta Simon tooTrakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed142-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed142-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ed142-206">В списке приложений hello выберите **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="ed142-206">In hello applications list, select **Trakopolis**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="ed142-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ed142-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ed142-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed142-210">Click **Add** button.</span></span> <span data-ttu-id="ed142-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed142-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ed142-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ed142-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed142-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ed142-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed142-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ed142-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed142-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ed142-216">Testing single sign-on</span></span>

<span data-ttu-id="ed142-217">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="ed142-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="ed142-218">При нажатии кнопки Trakopolis плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Trakopolis приложения.</span><span class="sxs-lookup"><span data-stu-id="ed142-218">When you click hello Trakopolis tile in hello Access Panel, you should get automatically signed-on tooyour Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed142-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ed142-219">Additional resources</span></span>

* [<span data-ttu-id="ed142-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed142-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed142-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed142-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

