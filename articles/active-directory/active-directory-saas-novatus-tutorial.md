---
title: "Руководство по интеграции Azure Active Directory с Novatus | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="25f87-103">Руководство по интеграции Azure Active Directory с Novatus</span><span class="sxs-lookup"><span data-stu-id="25f87-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="25f87-104">В этом учебнике вы узнаете, как toointegrate Novatus с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25f87-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25f87-105">Интеграция с Azure AD Novatus предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="25f87-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="25f87-106">Можно управлять в Azure AD, имеющего доступ tooNovatus</span><span class="sxs-lookup"><span data-stu-id="25f87-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="25f87-107">Можно включить на пользователей tooautomatically get вошедшего tooNovatus (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f87-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25f87-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="25f87-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="25f87-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25f87-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25f87-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="25f87-110">Prerequisites</span></span>

<span data-ttu-id="25f87-111">tooconfigure интеграция Azure AD с Novatus требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="25f87-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="25f87-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="25f87-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25f87-113">подписка Novatus с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="25f87-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25f87-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="25f87-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25f87-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="25f87-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25f87-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="25f87-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25f87-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25f87-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25f87-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="25f87-118">Scenario description</span></span>
<span data-ttu-id="25f87-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="25f87-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25f87-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="25f87-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25f87-121">Добавление Novatus из галереи hello</span><span class="sxs-lookup"><span data-stu-id="25f87-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="25f87-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f87-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="25f87-123">Добавление Novatus из галереи hello</span><span class="sxs-lookup"><span data-stu-id="25f87-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="25f87-124">tooconfigure hello интеграции Novatus в Azure AD, вы должны tooadd Novatus из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="25f87-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="25f87-125">**tooadd Novatus из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25f87-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="25f87-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="25f87-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25f87-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="25f87-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="25f87-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="25f87-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="25f87-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="25f87-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="25f87-133">Введите в поле поиска hello **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="25f87-133">In hello search box, type **Novatus**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="25f87-135">В панели результатов hello выберите **Novatus**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="25f87-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25f87-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f87-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25f87-138">В этом разделе описана настройка и проверка единого входа Azure AD в Novatus с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25f87-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25f87-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Novatus является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25f87-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="25f87-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Novatus должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="25f87-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="25f87-141">В Novatus, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="25f87-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="25f87-142">tooconfigure и теста Azure AD единого входа с Novatus, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="25f87-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25f87-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="25f87-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25f87-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="25f87-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25f87-145">**[Создание тестового пользователя Novatus](#creating-a-novatus-test-user)**  -toohave аналог Саймон Britta в Novatus, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="25f87-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="25f87-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="25f87-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25f87-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="25f87-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25f87-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f87-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25f87-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Novatus.</span><span class="sxs-lookup"><span data-stu-id="25f87-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="25f87-150">**tooconfigure Azure AD единого входа с Novatus, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25f87-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="25f87-151">В hello в hello портала Azure **Novatus** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="25f87-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="25f87-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="25f87-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="25f87-155">На hello **URL-адреса и домена Novatus** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="25f87-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="25f87-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="25f87-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25f87-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="25f87-158">This value is not real.</span></span> <span data-ttu-id="25f87-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="25f87-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="25f87-160">Обратитесь к [группа поддержки клиента Novatus](mailto:jvinci@novatusinc.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="25f87-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="25f87-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="25f87-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="25f87-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="25f87-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25f87-165">На hello **конфигурации Novatus** щелкните **Настройка Novatus** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="25f87-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="25f87-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="25f87-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="25f87-168">tooget SSO настроен для вашего приложения, обратитесь в службу вашей [Novatus поддержки](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="25f87-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="25f87-169">Присоединение hello **загружен сертификат** hello tooyour почты и совместное использование файла **URL-адреса метаданных** (**URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы**) с Novatus команды tooset копирование единого входа с их стороны.</span><span class="sxs-lookup"><span data-stu-id="25f87-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="25f87-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="25f87-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="25f87-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="25f87-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="25f87-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25f87-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25f87-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="25f87-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="25f87-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="25f87-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="25f87-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25f87-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25f87-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="25f87-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25f87-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="25f87-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25f87-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="25f87-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25f87-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="25f87-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25f87-185">а.</span><span class="sxs-lookup"><span data-stu-id="25f87-185">a.</span></span> <span data-ttu-id="25f87-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25f87-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25f87-187">b.</span><span class="sxs-lookup"><span data-stu-id="25f87-187">b.</span></span> <span data-ttu-id="25f87-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="25f87-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25f87-189">c.</span><span class="sxs-lookup"><span data-stu-id="25f87-189">c.</span></span> <span data-ttu-id="25f87-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="25f87-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="25f87-191">d.</span><span class="sxs-lookup"><span data-stu-id="25f87-191">d.</span></span> <span data-ttu-id="25f87-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="25f87-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="25f87-193">Создание тестового пользователя Novatus</span><span class="sxs-lookup"><span data-stu-id="25f87-193">Creating a Novatus test user</span></span>

<span data-ttu-id="25f87-194">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Novatus.</span><span class="sxs-lookup"><span data-stu-id="25f87-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="25f87-195">Приложение Novatus поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="25f87-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="25f87-196">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="25f87-196">There is no action item for you in this section.</span></span> <span data-ttu-id="25f87-197">Если он еще не существует во время попытки tooaccess Novatus создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="25f87-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="25f87-198">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Novatus поддержки](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="25f87-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="25f87-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="25f87-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="25f87-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNovatus доступа.</span><span class="sxs-lookup"><span data-stu-id="25f87-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="25f87-202">**tooassign tooNovatus Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="25f87-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="25f87-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="25f87-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="25f87-205">В списке приложений hello выберите **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="25f87-205">In hello applications list, select **Novatus**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="25f87-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="25f87-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="25f87-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="25f87-209">Click **Add** button.</span></span> <span data-ttu-id="25f87-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="25f87-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="25f87-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="25f87-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="25f87-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="25f87-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25f87-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="25f87-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25f87-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="25f87-215">Testing single sign-on</span></span>

<span data-ttu-id="25f87-216">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="25f87-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="25f87-217">При нажатии кнопки Novatus плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Novatus приложения.</span><span class="sxs-lookup"><span data-stu-id="25f87-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="25f87-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25f87-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25f87-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="25f87-219">Additional resources</span></span>

* [<span data-ttu-id="25f87-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25f87-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25f87-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25f87-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

