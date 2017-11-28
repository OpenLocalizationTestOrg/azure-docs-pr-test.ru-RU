---
title: "Руководство по интеграции Azure Active Directory с SECURE DELIVER | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ЗАЩИТИТЬ ДОСТАВКИ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 13699a9abb8be24054b0810a8178cd5ef170c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="84023-103">Руководство. Интеграция Azure Active Directory с SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="84023-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="84023-104">В этом учебнике вы узнаете, как обеспечивать безопасность toointegrate РАЗМЕЩАТЬ в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84023-104">In this tutorial, you learn how toointegrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84023-105">Интеграция защиты ДОСТАВКИ с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="84023-105">Integrating SECURE DELIVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84023-106">Можно управлять в Azure AD, имеющего доступ tooSECURE ДОСТАВКИ</span><span class="sxs-lookup"><span data-stu-id="84023-106">You can control in Azure AD who has access tooSECURE DELIVER</span></span>
- <span data-ttu-id="84023-107">Можно включить на пользователей tooautomatically get вошедшего tooSECURE ДОСТАВКИ (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="84023-107">You can enable your users tooautomatically get signed-on tooSECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84023-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="84023-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84023-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84023-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84023-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84023-110">Prerequisites</span></span>

<span data-ttu-id="84023-111">tooconfigure интеграция Azure AD с SECURE ДОСТАВКИ необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="84023-111">tooconfigure Azure AD integration with SECURE DELIVER, you need hello following items:</span></span>

- <span data-ttu-id="84023-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="84023-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84023-113">подписка SECURE DELIVER с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="84023-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84023-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="84023-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84023-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="84023-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84023-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="84023-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84023-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84023-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84023-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="84023-118">Scenario description</span></span>
<span data-ttu-id="84023-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="84023-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84023-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="84023-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84023-121">Добавление защиты ДОСТАВКИ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84023-121">Adding SECURE DELIVER from hello gallery</span></span>
2. <span data-ttu-id="84023-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84023-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-hello-gallery"></a><span data-ttu-id="84023-123">Добавление защиты ДОСТАВКИ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="84023-123">Adding SECURE DELIVER from hello gallery</span></span>
<span data-ttu-id="84023-124">tooconfigure hello интеграции защиты ДОСТАВКИ в Azure AD, вы должны tooadd SECURE ДОСТАВКИ из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="84023-124">tooconfigure hello integration of SECURE DELIVER into Azure AD, you need tooadd SECURE DELIVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84023-125">**tooadd SECURE ДОСТАВКИ из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="84023-125">**tooadd SECURE DELIVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84023-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="84023-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84023-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="84023-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84023-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84023-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="84023-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="84023-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="84023-133">Введите в поле поиска hello **SECURE ДОСТАВКИ**.</span><span class="sxs-lookup"><span data-stu-id="84023-133">In hello search box, type **SECURE DELIVER**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="84023-135">В панели результатов hello выберите **SECURE ДОСТАВКИ**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="84023-135">In hello results panel, select **SECURE DELIVER**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84023-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84023-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84023-138">В этом разделе описана настройка и проверка единого входа Azure AD в SECURE DELIVER с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84023-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84023-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SECURE ДОСТАВКИ является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84023-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SECURE DELIVER is tooa user in Azure AD.</span></span> <span data-ttu-id="84023-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SECURE ДОСТАВКИ должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="84023-140">In other words, a link relationship between an Azure AD user and hello related user in SECURE DELIVER needs toobe established.</span></span>

<span data-ttu-id="84023-141">В SECURE ДОСТАВИТЬ, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="84023-141">In SECURE DELIVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84023-142">tooconfigure и теста Azure AD единого входа с SECURE ДОСТАВКИ, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="84023-142">tooconfigure and test Azure AD single sign-on with SECURE DELIVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84023-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="84023-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84023-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="84023-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84023-145">**[Создание тестового пользователя SECURE ДОСТАВКИ](#creating-a-secure-deliver-test-user)**  -toohave аналог Саймон Britta в SECURE ДОСТАВКИ, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="84023-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - toohave a counterpart of Britta Simon in SECURE DELIVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84023-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="84023-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84023-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="84023-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84023-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="84023-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84023-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SECURE ДОСТАВКИ.</span><span class="sxs-lookup"><span data-stu-id="84023-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="84023-150">**Azure AD tooconfigure единого входа с SECURE ДОСТАВИТЬ, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="84023-150">**tooconfigure Azure AD single sign-on with SECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="84023-151">В hello в hello портала Azure **SECURE ДОСТАВКИ** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="84023-151">In hello Azure portal, on hello **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="84023-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="84023-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="84023-155">На hello **URL-адреса и безопасного домена ДОСТАВКИ** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84023-155">On hello **SECURE DELIVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="84023-157">а.</span><span class="sxs-lookup"><span data-stu-id="84023-157">a.</span></span> <span data-ttu-id="84023-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="84023-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="84023-159">b.</span><span class="sxs-lookup"><span data-stu-id="84023-159">b.</span></span> <span data-ttu-id="84023-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="84023-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84023-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="84023-161">These values are not real.</span></span> <span data-ttu-id="84023-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="84023-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84023-163">Обратитесь к [группы поддержки безопасного ДОСТАВКИ клиента](mailto:iw-sd-support@fujifilm.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="84023-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="84023-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="84023-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="84023-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="84023-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84023-168">На hello **SECURE конфигурации ДОСТАВКИ** щелкните **настройки безопасного ДОСТАВКИ** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="84023-168">On hello **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84023-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="84023-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="84023-171">tooconfigure единого входа на **SECURE ДОСТАВКИ** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[группы поддержки безопасного ДОСТАВКИ](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="84023-171">tooconfigure single sign-on on **SECURE DELIVER** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="84023-172">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="84023-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="84023-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="84023-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84023-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="84023-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84023-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84023-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84023-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="84023-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="84023-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="84023-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="84023-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="84023-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84023-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="84023-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84023-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="84023-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84023-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="84023-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84023-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="84023-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84023-188">а.</span><span class="sxs-lookup"><span data-stu-id="84023-188">a.</span></span> <span data-ttu-id="84023-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84023-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84023-190">b.</span><span class="sxs-lookup"><span data-stu-id="84023-190">b.</span></span> <span data-ttu-id="84023-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="84023-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84023-192">c.</span><span class="sxs-lookup"><span data-stu-id="84023-192">c.</span></span> <span data-ttu-id="84023-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="84023-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84023-194">d.</span><span class="sxs-lookup"><span data-stu-id="84023-194">d.</span></span> <span data-ttu-id="84023-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="84023-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="84023-196">Создание тестового пользователя в SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="84023-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="84023-197">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в SECURE ДОСТАВКИ.</span><span class="sxs-lookup"><span data-stu-id="84023-197">hello objective of this section is toocreate a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="84023-198">Работать с [группы поддержки безопасного ДОСТАВКИ](mailto:iw-sd-support@fujifilm.com) tooadd пользователей hello в hello SECURE ДОСТАВКИ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="84023-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) tooadd hello users in hello SECURE DELIVER account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="84023-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="84023-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="84023-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSECURE ДОСТАВКИ.</span><span class="sxs-lookup"><span data-stu-id="84023-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSECURE DELIVER.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="84023-202">**tooassign tooSECURE Britta Simon ДОСТАВКИ, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="84023-202">**tooassign Britta Simon tooSECURE DELIVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="84023-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="84023-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="84023-205">В списке приложений hello выберите **SECURE ДОСТАВКИ**.</span><span class="sxs-lookup"><span data-stu-id="84023-205">In hello applications list, select **SECURE DELIVER**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="84023-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="84023-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="84023-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="84023-209">Click **Add** button.</span></span> <span data-ttu-id="84023-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="84023-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="84023-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="84023-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84023-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="84023-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84023-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="84023-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84023-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="84023-215">Testing single sign-on</span></span>

<span data-ttu-id="84023-216">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="84023-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="84023-217">При нажатии кнопки hello SECURE ДОСТАВКИ плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour SECURE ДОСТАВКИ приложения.</span><span class="sxs-lookup"><span data-stu-id="84023-217">When you click hello SECURE DELIVER tile in hello Access Panel, you should get automatically signed-on tooyour SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84023-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84023-218">Additional resources</span></span>

* [<span data-ttu-id="84023-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84023-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84023-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84023-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

