---
title: "Руководство по интеграции Azure Active Directory с Skilljar | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Skilljar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c572f556-98a3-48e6-8e4c-e634b7a2ba70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f0f433d82a0b5510ec568ab610863bcade047697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skilljar"></a><span data-ttu-id="02466-103">Учебник. Интеграция Azure Active Directory с Skilljar</span><span class="sxs-lookup"><span data-stu-id="02466-103">Tutorial: Azure Active Directory integration with Skilljar</span></span>

<span data-ttu-id="02466-104">В этом учебнике вы узнаете, как toointegrate Skilljar с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02466-104">In this tutorial, you learn how toointegrate Skilljar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02466-105">Интеграция с Azure AD Skilljar предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="02466-105">Integrating Skilljar with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="02466-106">Можно управлять в Azure AD, имеющего доступ tooSkilljar</span><span class="sxs-lookup"><span data-stu-id="02466-106">You can control in Azure AD who has access tooSkilljar</span></span>
- <span data-ttu-id="02466-107">Можно включить на пользователей tooautomatically get вошедшего tooSkilljar (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="02466-107">You can enable your users tooautomatically get signed-on tooSkilljar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02466-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="02466-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="02466-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02466-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02466-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="02466-110">Prerequisites</span></span>

<span data-ttu-id="02466-111">tooconfigure интеграция Azure AD с Skilljar требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="02466-111">tooconfigure Azure AD integration with Skilljar, you need hello following items:</span></span>

- <span data-ttu-id="02466-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="02466-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02466-113">подписка Skilljar с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="02466-113">A Skilljar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02466-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="02466-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02466-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="02466-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02466-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="02466-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02466-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02466-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02466-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="02466-118">Scenario description</span></span>
<span data-ttu-id="02466-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="02466-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02466-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="02466-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02466-121">Добавление Skilljar из галереи hello</span><span class="sxs-lookup"><span data-stu-id="02466-121">Adding Skilljar from hello gallery</span></span>
2. <span data-ttu-id="02466-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02466-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skilljar-from-hello-gallery"></a><span data-ttu-id="02466-123">Добавление Skilljar из галереи hello</span><span class="sxs-lookup"><span data-stu-id="02466-123">Adding Skilljar from hello gallery</span></span>
<span data-ttu-id="02466-124">tooconfigure hello интеграции Skilljar в Azure AD, вы должны tooadd Skilljar из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="02466-124">tooconfigure hello integration of Skilljar into Azure AD, you need tooadd Skilljar from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="02466-125">**tooadd Skilljar из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="02466-125">**tooadd Skilljar from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="02466-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="02466-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02466-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="02466-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="02466-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="02466-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="02466-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="02466-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="02466-133">Введите в поле поиска hello **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="02466-133">In hello search box, type **Skilljar**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_search.png)

5. <span data-ttu-id="02466-135">В панели результатов hello выберите **Skilljar**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="02466-135">In hello results panel, select **Skilljar**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02466-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02466-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02466-138">В этом разделе описана настройка и проверка единого входа Azure AD в Skilljar с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02466-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02466-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Skilljar является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02466-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skilljar is tooa user in Azure AD.</span></span> <span data-ttu-id="02466-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Skilljar должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="02466-140">In other words, a link relationship between an Azure AD user and hello related user in Skilljar needs toobe established.</span></span>

<span data-ttu-id="02466-141">В Skilljar, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="02466-141">In Skilljar, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="02466-142">tooconfigure и теста Azure AD единого входа с Skilljar, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="02466-142">tooconfigure and test Azure AD single sign-on with Skilljar, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="02466-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="02466-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="02466-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="02466-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02466-145">**[Создание тестового пользователя Skilljar](#creating-a-skilljar-test-user)**  -toohave аналог Саймон Britta в Skilljar, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="02466-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - toohave a counterpart of Britta Simon in Skilljar that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="02466-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="02466-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02466-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="02466-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02466-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02466-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02466-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Skilljar.</span><span class="sxs-lookup"><span data-stu-id="02466-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skilljar application.</span></span>

<span data-ttu-id="02466-150">**tooconfigure Azure AD единого входа с Skilljar, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="02466-150">**tooconfigure Azure AD single sign-on with Skilljar, perform hello following steps:**</span></span>

1. <span data-ttu-id="02466-151">В hello в hello портала Azure **Skilljar** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="02466-151">In hello Azure portal, on hello **Skilljar** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="02466-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="02466-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_samlbase.png)

3. <span data-ttu-id="02466-155">На hello **URL-адреса и домена Skilljar** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="02466-155">On hello **Skilljar Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_url.png)

    <span data-ttu-id="02466-157">а.</span><span class="sxs-lookup"><span data-stu-id="02466-157">a.</span></span> <span data-ttu-id="02466-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="02466-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.skilljar.com/`</span></span>

    <span data-ttu-id="02466-159">b.</span><span class="sxs-lookup"><span data-stu-id="02466-159">b.</span></span> <span data-ttu-id="02466-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="02466-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.skilljar.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02466-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="02466-161">These values are not real.</span></span> <span data-ttu-id="02466-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="02466-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="02466-163">Обратитесь к [группа поддержки клиента Skilljar](http://support.skilljar.com/hc/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="02466-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) tooget these values.</span></span> 
 
4. <span data-ttu-id="02466-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="02466-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_certificate.png) 

5. <span data-ttu-id="02466-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="02466-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skilljar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02466-168">tooconfigure единого входа на **Skilljar** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, и **значение формата идентификатора имени — urn: oasis: имена: tc: SAML:1.1:nameid-формат: emailAddress** слишком[Skilljar поддержки](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="02466-168">tooconfigure single sign-on on **Skilljar** side, you need toosend hello downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** too[Skilljar support team](http://support.skilljar.com/hc/).</span></span> <span data-ttu-id="02466-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="02466-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="02466-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="02466-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="02466-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="02466-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="02466-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02466-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02466-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="02466-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="02466-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="02466-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="02466-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="02466-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="02466-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="02466-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02466-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="02466-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02466-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="02466-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02466-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="02466-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02466-185">а.</span><span class="sxs-lookup"><span data-stu-id="02466-185">a.</span></span> <span data-ttu-id="02466-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02466-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02466-187">b.</span><span class="sxs-lookup"><span data-stu-id="02466-187">b.</span></span> <span data-ttu-id="02466-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02466-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02466-189">c.</span><span class="sxs-lookup"><span data-stu-id="02466-189">c.</span></span> <span data-ttu-id="02466-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="02466-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="02466-191">d.</span><span class="sxs-lookup"><span data-stu-id="02466-191">d.</span></span> <span data-ttu-id="02466-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="02466-192">Click **Create**.</span></span>
 
### <a name="creating-a-skilljar-test-user"></a><span data-ttu-id="02466-193">Создание тестового пользователя Skilljar</span><span class="sxs-lookup"><span data-stu-id="02466-193">Creating a Skilljar test user</span></span>

<span data-ttu-id="02466-194">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Skilljar.</span><span class="sxs-lookup"><span data-stu-id="02466-194">hello objective of this section is toocreate a user called Britta Simon in Skilljar.</span></span> <span data-ttu-id="02466-195">Приложение Skilljar поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="02466-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="02466-196">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="02466-196">There is no action item for you in this section.</span></span> <span data-ttu-id="02466-197">Новый пользователь создается во время попытки tooaccess Skilljar, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="02466-197">A new user is created during an attempt tooaccess Skilljar if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="02466-198">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Skilljar поддержки](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="02466-198">If you need toocreate a user manually, you need toocontact hello [Skilljar support team](http://support.skilljar.com/hc/).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="02466-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="02466-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="02466-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSkilljar доступа.</span><span class="sxs-lookup"><span data-stu-id="02466-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkilljar.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="02466-202">**tooassign tooSkilljar Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="02466-202">**tooassign Britta Simon tooSkilljar, perform hello following steps:**</span></span>

1. <span data-ttu-id="02466-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="02466-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="02466-205">В списке приложений hello выберите **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="02466-205">In hello applications list, select **Skilljar**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_app.png) 

3. <span data-ttu-id="02466-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="02466-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="02466-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="02466-209">Click **Add** button.</span></span> <span data-ttu-id="02466-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="02466-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="02466-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="02466-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="02466-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="02466-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02466-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="02466-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02466-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="02466-215">Testing single sign-on</span></span>

<span data-ttu-id="02466-216">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="02466-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="02466-217">При нажатии кнопки hello Skilljar плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Skilljar приложения.</span><span class="sxs-lookup"><span data-stu-id="02466-217">When you click hello Skilljar tile in hello Access Panel, you should get automatically signed-on tooyour Skilljar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02466-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="02466-218">Additional resources</span></span>

* [<span data-ttu-id="02466-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02466-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02466-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02466-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_203.png

