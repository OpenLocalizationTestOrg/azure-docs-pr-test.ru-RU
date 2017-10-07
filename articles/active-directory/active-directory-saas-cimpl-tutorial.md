---
title: "Учебник. Интеграция Azure Active Directory с Cimpl | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cimpl."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 0b993f2b58aaeac24e657060fb31651edc847f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="62e83-103">Руководство. Интеграция Azure Active Directory с Cimpl</span><span class="sxs-lookup"><span data-stu-id="62e83-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="62e83-104">В этом учебнике вы узнаете, как toointegrate Cimpl с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62e83-104">In this tutorial, you learn how toointegrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62e83-105">Интеграция с Azure AD Cimpl предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="62e83-105">Integrating Cimpl with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62e83-106">Можно управлять в Azure AD, имеющего доступ tooCimpl</span><span class="sxs-lookup"><span data-stu-id="62e83-106">You can control in Azure AD who has access tooCimpl</span></span>
- <span data-ttu-id="62e83-107">Можно включить на пользователей tooautomatically get вошедшего tooCimpl (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e83-107">You can enable your users tooautomatically get signed-on tooCimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62e83-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="62e83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62e83-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62e83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62e83-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62e83-110">Prerequisites</span></span>

<span data-ttu-id="62e83-111">tooconfigure интеграция Azure AD с Cimpl требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="62e83-111">tooconfigure Azure AD integration with Cimpl, you need hello following items:</span></span>

- <span data-ttu-id="62e83-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="62e83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62e83-113">подписка на Cimpl с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="62e83-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62e83-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="62e83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62e83-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="62e83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62e83-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="62e83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62e83-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62e83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62e83-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="62e83-118">Scenario description</span></span>
<span data-ttu-id="62e83-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="62e83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62e83-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="62e83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62e83-121">Добавление Cimpl из галереи hello</span><span class="sxs-lookup"><span data-stu-id="62e83-121">Adding Cimpl from hello gallery</span></span>
2. <span data-ttu-id="62e83-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-hello-gallery"></a><span data-ttu-id="62e83-123">Добавление Cimpl из галереи hello</span><span class="sxs-lookup"><span data-stu-id="62e83-123">Adding Cimpl from hello gallery</span></span>
<span data-ttu-id="62e83-124">tooconfigure hello интеграции Cimpl в Azure AD, вы должны tooadd Cimpl из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="62e83-124">tooconfigure hello integration of Cimpl into Azure AD, you need tooadd Cimpl from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62e83-125">**tooadd Cimpl из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="62e83-125">**tooadd Cimpl from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62e83-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="62e83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62e83-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="62e83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62e83-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e83-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="62e83-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="62e83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="62e83-133">Введите в поле поиска hello **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="62e83-133">In hello search box, type **Cimpl**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_search.png)

5. <span data-ttu-id="62e83-135">В панели результатов hello выберите **Cimpl**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="62e83-135">In hello results panel, select **Cimpl**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62e83-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62e83-138">В этом разделе описана настройка и проверка единого входа Azure AD для приложения Cimpl и тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62e83-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62e83-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Cimpl является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cimpl is tooa user in Azure AD.</span></span> <span data-ttu-id="62e83-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Cimpl должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="62e83-140">In other words, a link relationship between an Azure AD user and hello related user in Cimpl needs toobe established.</span></span>

<span data-ttu-id="62e83-141">В Cimpl, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="62e83-141">In Cimpl, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="62e83-142">tooconfigure и теста Azure AD единого входа с Cimpl, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="62e83-142">tooconfigure and test Azure AD single sign-on with Cimpl, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62e83-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="62e83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62e83-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="62e83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62e83-145">**[Создание тестового пользователя Cimpl](#creating-a-cimpl-test-user)**  -toohave аналог Саймон Britta в Cimpl, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="62e83-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - toohave a counterpart of Britta Simon in Cimpl that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="62e83-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="62e83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62e83-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62e83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62e83-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62e83-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Cimpl.</span><span class="sxs-lookup"><span data-stu-id="62e83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="62e83-150">**tooconfigure Azure AD единого входа с Cimpl, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="62e83-150">**tooconfigure Azure AD single sign-on with Cimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="62e83-151">В hello в hello портала Azure **Cimpl** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="62e83-151">In hello Azure portal, on hello **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="62e83-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="62e83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_samlbase.png)

3. <span data-ttu-id="62e83-155">На hello **URL-адреса и домена Cimpl** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="62e83-155">On hello **Cimpl Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="62e83-157">а.</span><span class="sxs-lookup"><span data-stu-id="62e83-157">a.</span></span> <span data-ttu-id="62e83-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="62e83-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="62e83-159">b.</span><span class="sxs-lookup"><span data-stu-id="62e83-159">b.</span></span> <span data-ttu-id="62e83-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="62e83-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62e83-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="62e83-161">These values are not real.</span></span> <span data-ttu-id="62e83-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="62e83-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="62e83-163">Обратитесь в службу Cimpl на **+1 866-982-8250** tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="62e83-163">Contact Cimpl team at **+1 866-982-8250** tooget these values.</span></span> 
 
4. <span data-ttu-id="62e83-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="62e83-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_certificate.png) 

5. <span data-ttu-id="62e83-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="62e83-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62e83-168">На hello **конфигурации Cimpl** щелкните **Настройка Cimpl** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="62e83-168">On hello **Cimpl Configuration** section, click **Configure Cimpl** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="62e83-169">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="62e83-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_configure.png) 

7. <span data-ttu-id="62e83-171">tooconfigure единого входа на **Cimpl** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **идентификатор сущности SAML и SAML единого входа URL-адрес службы** tooCimpl в поддерживает **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="62e83-171">tooconfigure single sign-on on **Cimpl** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** tooCimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="62e83-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="62e83-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62e83-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="62e83-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62e83-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62e83-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62e83-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e83-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="62e83-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="62e83-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="62e83-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="62e83-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62e83-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="62e83-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62e83-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="62e83-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62e83-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="62e83-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62e83-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="62e83-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62e83-187">а.</span><span class="sxs-lookup"><span data-stu-id="62e83-187">a.</span></span> <span data-ttu-id="62e83-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62e83-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62e83-189">b.</span><span class="sxs-lookup"><span data-stu-id="62e83-189">b.</span></span> <span data-ttu-id="62e83-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62e83-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62e83-191">c.</span><span class="sxs-lookup"><span data-stu-id="62e83-191">c.</span></span> <span data-ttu-id="62e83-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="62e83-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62e83-193">d.</span><span class="sxs-lookup"><span data-stu-id="62e83-193">d.</span></span> <span data-ttu-id="62e83-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="62e83-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="62e83-195">Создание тестового пользователя Cimpl</span><span class="sxs-lookup"><span data-stu-id="62e83-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="62e83-196">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Cimpl.</span><span class="sxs-lookup"><span data-stu-id="62e83-196">hello objective of this section is toocreate a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="62e83-197">Работать с технической поддержки Cimpl **+1 866-982-8250** tooadd пользователей hello в hello Cimpl учетной записи.</span><span class="sxs-lookup"><span data-stu-id="62e83-197">Work with Cimpl support at **+1 866-982-8250** tooadd hello users in hello Cimpl account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62e83-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="62e83-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62e83-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCimpl доступа.</span><span class="sxs-lookup"><span data-stu-id="62e83-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCimpl.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="62e83-201">**tooassign tooCimpl Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="62e83-201">**tooassign Britta Simon tooCimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="62e83-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e83-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="62e83-204">В списке приложений hello выберите **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="62e83-204">In hello applications list, select **Cimpl**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_app.png) 

3. <span data-ttu-id="62e83-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="62e83-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="62e83-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62e83-208">Click **Add** button.</span></span> <span data-ttu-id="62e83-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="62e83-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="62e83-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="62e83-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62e83-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="62e83-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62e83-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="62e83-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62e83-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="62e83-214">Testing single sign-on</span></span>

<span data-ttu-id="62e83-215">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="62e83-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  <span data-ttu-id="62e83-216">При нажатии кнопки hello Cimpl плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Cimpl приложения.</span><span class="sxs-lookup"><span data-stu-id="62e83-216">When you click hello Cimpl tile in hello Access Panel, you should get automatically signed-on tooyour Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="62e83-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="62e83-217">Additional resources</span></span>

* [<span data-ttu-id="62e83-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62e83-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62e83-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62e83-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png

