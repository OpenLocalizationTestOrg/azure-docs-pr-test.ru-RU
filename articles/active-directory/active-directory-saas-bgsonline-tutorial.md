---
title: "Руководство по интеграции Azure Active Directory с BGS Online | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ФОНЫ Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="5a319-103">Учебник. Интеграция Azure Active Directory с BGS Online</span><span class="sxs-lookup"><span data-stu-id="5a319-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="5a319-104">В этом учебнике вы узнаете, как toointegrate ФОНЫ Online с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a319-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a319-105">Интеграция ФОНЫ Online с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5a319-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a319-106">Можно управлять в Azure AD, имеющего tooBGS доступ через Интернет</span><span class="sxs-lookup"><span data-stu-id="5a319-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="5a319-107">Можно включить на пользователей tooautomatically get вошедшего tooBGS сети (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a319-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a319-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5a319-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a319-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a319-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a319-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a319-110">Prerequisites</span></span>

<span data-ttu-id="5a319-111">tooconfigure интеграция Azure AD с ФОНЫ Online требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5a319-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="5a319-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5a319-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a319-113">подписка BGS Online с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5a319-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a319-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5a319-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a319-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5a319-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a319-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5a319-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a319-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a319-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a319-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5a319-118">Scenario description</span></span>
<span data-ttu-id="5a319-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5a319-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a319-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5a319-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a319-121">Добавление документации ФОНЫ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5a319-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="5a319-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a319-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="5a319-123">Добавление документации ФОНЫ из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5a319-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="5a319-124">tooconfigure hello интеграции ФОНЫ сети в Azure AD, вы должны tooadd ФОНЫ сети из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5a319-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a319-125">**tooadd ФОНЫ Online из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="5a319-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a319-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5a319-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a319-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5a319-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a319-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5a319-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5a319-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5a319-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5a319-133">Введите в поле поиска hello **Online ФОНЫ**.</span><span class="sxs-lookup"><span data-stu-id="5a319-133">In hello search box, type **BGS Online**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="5a319-135">В панели результатов hello, выберите **Online ФОНЫ**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5a319-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a319-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a319-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a319-138">В этом разделе описана настройка и проверка единого входа Azure AD в BGS Online с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a319-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a319-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello ФОНЫ документации является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a319-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="5a319-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello ФОНЫ документации должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5a319-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="5a319-141">В документации ФОНЫ присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5a319-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a319-142">tooconfigure и тестирования Azure AD единого входа с ФОНЫ Online, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5a319-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a319-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5a319-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a319-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5a319-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a319-145">**[Создание тестового пользователя ФОНЫ Online](#creating-a-bgs-online-test-user)**  -toohave аналог Саймон Britta ФОНЫ документации, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5a319-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a319-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5a319-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a319-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5a319-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a319-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a319-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a319-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ФОНЫ Online.</span><span class="sxs-lookup"><span data-stu-id="5a319-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="5a319-150">**tooconfigure Azure AD единого входа с Online ФОНЫ выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a319-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a319-151">В hello в hello портала Azure **Online ФОНЫ** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5a319-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5a319-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5a319-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="5a319-155">На hello **URL-адреса и домена ФОНЫ** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5a319-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="5a319-157">а.</span><span class="sxs-lookup"><span data-stu-id="5a319-157">a.</span></span> <span data-ttu-id="5a319-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5a319-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="5a319-159">Для рабочей среды следует использовать шаблон `https://<company name>.millwardbrown.report`.</span><span class="sxs-lookup"><span data-stu-id="5a319-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="5a319-160">Для тестовой среды следует использовать шаблон `https://millwardbrown.marketingtracker.nl/mt5/`.</span><span class="sxs-lookup"><span data-stu-id="5a319-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="5a319-161">b.</span><span class="sxs-lookup"><span data-stu-id="5a319-161">b.</span></span> <span data-ttu-id="5a319-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5a319-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="5a319-163">Для рабочей среды следует использовать шаблон `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`.</span><span class="sxs-lookup"><span data-stu-id="5a319-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="5a319-164">Для тестовой среды следует использовать шаблон `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`.</span><span class="sxs-lookup"><span data-stu-id="5a319-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a319-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5a319-165">These values are not real.</span></span> <span data-ttu-id="5a319-166">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5a319-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5a319-167">Обратитесь к [ФОНЫ интерактивной поддержки](mailTo:bgsdashboardteam@millwardbrown.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5a319-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="5a319-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5a319-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="5a319-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5a319-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a319-172">На hello **конфигурации оперативной ФОНЫ** щелкните **Настройка ФОНЫ Online** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5a319-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a319-173">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5a319-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="5a319-175">tooconfigure единого входа на **Online ФОНЫ** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **SAML единого входа URL-адрес службы** слишком[ФОНЫ Поддержка команды](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="5a319-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="5a319-176">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5a319-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a319-177">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5a319-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a319-178">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a319-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a319-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a319-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a319-180">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5a319-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5a319-182">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5a319-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a319-183">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5a319-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a319-185">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5a319-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a319-187">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5a319-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a319-189">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5a319-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a319-191">а.</span><span class="sxs-lookup"><span data-stu-id="5a319-191">a.</span></span> <span data-ttu-id="5a319-192">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a319-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a319-193">b.</span><span class="sxs-lookup"><span data-stu-id="5a319-193">b.</span></span> <span data-ttu-id="5a319-194">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5a319-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a319-195">c.</span><span class="sxs-lookup"><span data-stu-id="5a319-195">c.</span></span> <span data-ttu-id="5a319-196">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5a319-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a319-197">d.</span><span class="sxs-lookup"><span data-stu-id="5a319-197">d.</span></span> <span data-ttu-id="5a319-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5a319-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="5a319-199">Создание тестового пользователя BGS Online</span><span class="sxs-lookup"><span data-stu-id="5a319-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="5a319-200">В этом разделе описано, как создать пользователя Britta Simon в BGS Online.</span><span class="sxs-lookup"><span data-stu-id="5a319-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="5a319-201">Работать с [ФОНЫ интерактивной поддержки](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello пользователей в сети ФОНЫ платформы hello.</span><span class="sxs-lookup"><span data-stu-id="5a319-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a319-202">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5a319-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a319-203">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBGS доступа через Интернет.</span><span class="sxs-lookup"><span data-stu-id="5a319-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5a319-205">**tooassign Britta Simon tooBGS через Интернет, выполнять hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="5a319-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a319-206">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5a319-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5a319-208">В списке приложений hello выберите **Online ФОНЫ**.</span><span class="sxs-lookup"><span data-stu-id="5a319-208">In hello applications list, select **BGS Online**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="5a319-210">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5a319-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5a319-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5a319-212">Click **Add** button.</span></span> <span data-ttu-id="5a319-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5a319-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5a319-215">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5a319-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a319-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5a319-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a319-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5a319-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a319-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5a319-218">Testing single sign-on</span></span>

<span data-ttu-id="5a319-219">В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5a319-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a319-220">При нажатии кнопки hello ФОНЫ Online плитки в панели доступа hello, вы должны получить tooyour автоматически вошедшего ФОНЫ интерактивных приложений.</span><span class="sxs-lookup"><span data-stu-id="5a319-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a319-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5a319-221">Additional resources</span></span>

* [<span data-ttu-id="5a319-222">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a319-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a319-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5a319-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

