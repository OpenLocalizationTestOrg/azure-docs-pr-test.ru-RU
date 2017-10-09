---
title: "Руководство по интеграции Azure Active Directory с MCM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и MCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 6fbb3c641725bed1e7c73ee78129efb86979839e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="8044f-103">Руководство. Интеграция Azure Active Directory с МСМ</span><span class="sxs-lookup"><span data-stu-id="8044f-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="8044f-104">В этом учебнике вы узнаете, как toointegrate MCM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8044f-104">In this tutorial, you learn how toointegrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8044f-105">Интеграция с Azure AD MCM предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8044f-105">Integrating MCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8044f-106">Можно управлять в Azure AD, имеющего доступ tooMCM</span><span class="sxs-lookup"><span data-stu-id="8044f-106">You can control in Azure AD who has access tooMCM</span></span>
- <span data-ttu-id="8044f-107">Можно включить на пользователей tooautomatically get вошедшего tooMCM (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8044f-107">You can enable your users tooautomatically get signed-on tooMCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8044f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8044f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8044f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8044f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8044f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8044f-110">Prerequisites</span></span>

<span data-ttu-id="8044f-111">tooconfigure интеграция Azure AD с MCM требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8044f-111">tooconfigure Azure AD integration with MCM, you need hello following items:</span></span>

- <span data-ttu-id="8044f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8044f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8044f-113">подписка на MCM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8044f-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8044f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8044f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8044f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8044f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8044f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8044f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8044f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8044f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8044f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8044f-118">Scenario description</span></span>
<span data-ttu-id="8044f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8044f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8044f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8044f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8044f-121">Добавление MCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8044f-121">Adding MCM from hello gallery</span></span>
2. <span data-ttu-id="8044f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8044f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-hello-gallery"></a><span data-ttu-id="8044f-123">Добавление MCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8044f-123">Adding MCM from hello gallery</span></span>
<span data-ttu-id="8044f-124">tooconfigure hello интеграции MCM в Azure AD, вы должны tooadd MCM из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8044f-124">tooconfigure hello integration of MCM into Azure AD, you need tooadd MCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8044f-125">**tooadd MCM из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8044f-125">**tooadd MCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8044f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8044f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8044f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8044f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8044f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8044f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8044f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8044f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8044f-133">Введите в поле поиска hello **MCM**.</span><span class="sxs-lookup"><span data-stu-id="8044f-133">In hello search box, type **MCM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_search.png)

5. <span data-ttu-id="8044f-135">В панели результатов hello выберите **MCM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8044f-135">In hello results panel, select **MCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8044f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8044f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8044f-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение MCM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8044f-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8044f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в MCM является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8044f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MCM is tooa user in Azure AD.</span></span> <span data-ttu-id="8044f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в MCM должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8044f-140">In other words, a link relationship between an Azure AD user and hello related user in MCM needs toobe established.</span></span>

<span data-ttu-id="8044f-141">В MCM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8044f-141">In MCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8044f-142">tooconfigure и теста Azure AD единого входа с MCM, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8044f-142">tooconfigure and test Azure AD single sign-on with MCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8044f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8044f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8044f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8044f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8044f-145">**[Создание MCM тестовый пользователь](#creating-a-mcm-test-user)**  -toohave аналог Саймон Britta в MCM, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8044f-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - toohave a counterpart of Britta Simon in MCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8044f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8044f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8044f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8044f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8044f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8044f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8044f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении MCM.</span><span class="sxs-lookup"><span data-stu-id="8044f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="8044f-150">**tooconfigure Azure AD единого входа с MCM, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8044f-150">**tooconfigure Azure AD single sign-on with MCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="8044f-151">В hello в hello портала Azure **MCM** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8044f-151">In hello Azure portal, on hello **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8044f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8044f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_samlbase.png)

3. <span data-ttu-id="8044f-155">На hello **URL-адреса и домена MCM** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8044f-155">On hello **MCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="8044f-157">а.</span><span class="sxs-lookup"><span data-stu-id="8044f-157">a.</span></span> <span data-ttu-id="8044f-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="8044f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="8044f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8044f-159">b.</span></span> <span data-ttu-id="8044f-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8044f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8044f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8044f-161">These values are not real.</span></span> <span data-ttu-id="8044f-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8044f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8044f-163">Обратитесь к [группа поддержки клиента MCM](http://mcmtechnology.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="8044f-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8044f-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8044f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_certificate.png) 

5. <span data-ttu-id="8044f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8044f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="8044f-168">tooconfigure единого входа на **MCM** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[MCM поддержки](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="8044f-168">tooconfigure single sign-on on **MCM** side, you need toosend hello downloaded **Metadata XML** too[MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="8044f-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="8044f-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8044f-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8044f-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8044f-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8044f-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8044f-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8044f-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8044f-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8044f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8044f-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8044f-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8044f-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8044f-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8044f-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8044f-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8044f-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8044f-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8044f-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8044f-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8044f-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8044f-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8044f-185">а.</span><span class="sxs-lookup"><span data-stu-id="8044f-185">a.</span></span> <span data-ttu-id="8044f-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8044f-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8044f-187">b.</span><span class="sxs-lookup"><span data-stu-id="8044f-187">b.</span></span> <span data-ttu-id="8044f-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8044f-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8044f-189">c.</span><span class="sxs-lookup"><span data-stu-id="8044f-189">c.</span></span> <span data-ttu-id="8044f-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8044f-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8044f-191">d.</span><span class="sxs-lookup"><span data-stu-id="8044f-191">d.</span></span> <span data-ttu-id="8044f-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8044f-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="8044f-193">Создание тестового пользователя MCM</span><span class="sxs-lookup"><span data-stu-id="8044f-193">Creating a MCM test user</span></span>

<span data-ttu-id="8044f-194">В этом разделе описано, как создать пользователя Britta Simon в приложении MCM.</span><span class="sxs-lookup"><span data-stu-id="8044f-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="8044f-195">Работать с [MCM поддержки](http://mcmtechnology.com/support/) tooadd hello пользователей на платформе MCM hello.</span><span class="sxs-lookup"><span data-stu-id="8044f-195">Work with [MCM support team](http://mcmtechnology.com/support/) tooadd hello users in hello MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="8044f-196">Можно использовать любые другие MCM пользователя средства создания учетных записей или интерфейсы API, предоставляемые MCM tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="8044f-196">You can use any other MCM user account creation tools or APIs provided by MCM tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8044f-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8044f-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8044f-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMCM доступа.</span><span class="sxs-lookup"><span data-stu-id="8044f-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMCM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8044f-200">**tooassign tooMCM Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8044f-200">**tooassign Britta Simon tooMCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="8044f-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8044f-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8044f-203">В списке приложений hello выберите **MCM**.</span><span class="sxs-lookup"><span data-stu-id="8044f-203">In hello applications list, select **MCM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_app.png) 

3. <span data-ttu-id="8044f-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8044f-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8044f-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8044f-207">Click **Add** button.</span></span> <span data-ttu-id="8044f-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8044f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8044f-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8044f-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8044f-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8044f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8044f-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8044f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8044f-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8044f-213">Testing single sign-on</span></span>

<span data-ttu-id="8044f-214">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="8044f-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8044f-215">При нажатии кнопки MCM плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour MCM приложения.</span><span class="sxs-lookup"><span data-stu-id="8044f-215">When you click hello MCM tile in hello Access Panel, you should get automatically signed-on tooyour MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8044f-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8044f-216">Additional resources</span></span>

* [<span data-ttu-id="8044f-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8044f-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8044f-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8044f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_203.png

