---
title: "Руководство по интеграции Azure Active Directory с RolePoint | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="940a1-103">Руководство по интеграции Azure Active Directory с RolePoint</span><span class="sxs-lookup"><span data-stu-id="940a1-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="940a1-104">В этом учебнике вы узнаете, как toointegrate RolePoint с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="940a1-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="940a1-105">Интеграция с Azure AD RolePoint предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="940a1-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="940a1-106">Можно управлять в Azure AD, имеющего доступ tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="940a1-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="940a1-107">Можно включить на пользователей tooautomatically get вошедшего tooRolePoint (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="940a1-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="940a1-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="940a1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="940a1-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="940a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="940a1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="940a1-110">Prerequisites</span></span>

<span data-ttu-id="940a1-111">tooconfigure интеграция Azure AD с RolePoint требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="940a1-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="940a1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="940a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="940a1-113">подписка RolePoint с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="940a1-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="940a1-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="940a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="940a1-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="940a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="940a1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="940a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="940a1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="940a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="940a1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="940a1-118">Scenario description</span></span>
<span data-ttu-id="940a1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="940a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="940a1-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="940a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="940a1-121">Добавление RolePoint из галереи hello</span><span class="sxs-lookup"><span data-stu-id="940a1-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="940a1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="940a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="940a1-123">Добавление RolePoint из галереи hello</span><span class="sxs-lookup"><span data-stu-id="940a1-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="940a1-124">tooconfigure hello интеграции RolePoint в Azure AD, вы должны tooadd RolePoint из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="940a1-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="940a1-125">**tooadd RolePoint из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="940a1-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="940a1-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="940a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="940a1-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="940a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="940a1-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="940a1-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="940a1-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="940a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="940a1-133">Введите в поле поиска hello **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="940a1-133">In hello search box, type **RolePoint**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="940a1-135">В панели результатов hello выберите **RolePoint**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="940a1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="940a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="940a1-138">В этом разделе мы выполним настройку и проверку единого входа Azure AD в RolePoint с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="940a1-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="940a1-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в RolePoint является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="940a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="940a1-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в RolePoint должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="940a1-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="940a1-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в RolePoint.</span><span class="sxs-lookup"><span data-stu-id="940a1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="940a1-142">tooconfigure и теста Azure AD единого входа с RolePoint, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="940a1-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="940a1-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="940a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="940a1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="940a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="940a1-145">**[Создание тестового пользователя RolePoint](#creating-a-rolepoint-test-user)**  -toohave аналог Саймон Britta в RolePoint, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="940a1-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="940a1-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="940a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="940a1-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="940a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="940a1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="940a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="940a1-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RolePoint.</span><span class="sxs-lookup"><span data-stu-id="940a1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="940a1-150">**tooconfigure Azure AD единого входа с RolePoint, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="940a1-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="940a1-151">В hello в hello портала Azure **RolePoint** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="940a1-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="940a1-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="940a1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="940a1-155">На hello **URL-адреса и домена RolePoint** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="940a1-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="940a1-157">а.</span><span class="sxs-lookup"><span data-stu-id="940a1-157">a.</span></span> <span data-ttu-id="940a1-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="940a1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="940a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="940a1-159">b.</span></span> <span data-ttu-id="940a1-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="940a1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="940a1-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-161">These values are not hello real.</span></span> <span data-ttu-id="940a1-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="940a1-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="940a1-163">Здесь мы советуем вам toouse hello уникальное значение строки в hello Identifier.Contact [RolePoint поддержки](mailto:info@rolepoint.com) tooget значение hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="940a1-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="940a1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="940a1-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="940a1-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="940a1-168">tooconfigure единого входа на **RolePoint** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[RolePoint поддержки](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="940a1-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="940a1-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="940a1-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="940a1-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="940a1-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="940a1-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="940a1-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="940a1-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="940a1-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="940a1-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="940a1-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="940a1-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="940a1-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="940a1-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="940a1-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="940a1-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="940a1-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="940a1-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="940a1-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="940a1-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="940a1-184">а.</span><span class="sxs-lookup"><span data-stu-id="940a1-184">a.</span></span> <span data-ttu-id="940a1-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="940a1-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="940a1-186">b.</span><span class="sxs-lookup"><span data-stu-id="940a1-186">b.</span></span> <span data-ttu-id="940a1-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="940a1-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="940a1-188">c.</span><span class="sxs-lookup"><span data-stu-id="940a1-188">c.</span></span> <span data-ttu-id="940a1-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="940a1-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="940a1-190">d.</span><span class="sxs-lookup"><span data-stu-id="940a1-190">d.</span></span> <span data-ttu-id="940a1-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="940a1-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="940a1-192">Создание тестового пользователя RolePoint</span><span class="sxs-lookup"><span data-stu-id="940a1-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="940a1-193">В этом разделе описано, как создать пользователя Britta Simon в приложении RolePoint.</span><span class="sxs-lookup"><span data-stu-id="940a1-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="940a1-194">Работать с [RolePoint поддержки](mailto:info@rolepoint.com) tooadd hello пользователей на платформе RolePoint hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="940a1-195">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="940a1-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="940a1-196">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRolePoint доступа.</span><span class="sxs-lookup"><span data-stu-id="940a1-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="940a1-198">**tooassign tooRolePoint Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="940a1-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="940a1-199">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="940a1-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="940a1-201">В списке приложений hello выберите **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="940a1-201">In hello applications list, select **RolePoint**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="940a1-203">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="940a1-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="940a1-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="940a1-205">Click **Add** button.</span></span> <span data-ttu-id="940a1-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="940a1-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="940a1-208">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="940a1-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="940a1-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="940a1-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="940a1-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="940a1-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="940a1-211">Testing single sign-on</span></span>

<span data-ttu-id="940a1-212">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="940a1-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="940a1-213">При нажатии кнопки hello RolePoint плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour RolePoint приложения.</span><span class="sxs-lookup"><span data-stu-id="940a1-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="940a1-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="940a1-214">Additional resources</span></span>

* [<span data-ttu-id="940a1-215">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="940a1-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="940a1-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="940a1-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

