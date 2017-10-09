---
title: "Руководство по интеграции Azure Active Directory с приложением \"Люди\" | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и пользователей."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: d540c31867c92c4dc09db9c0833f8a8a7c02b371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="4bd28-103">Руководство. Интеграция Azure Active Directory с приложением "Люди"</span><span class="sxs-lookup"><span data-stu-id="4bd28-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="4bd28-104">В этом учебнике вы узнаете, как пользователи toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bd28-104">In this tutorial, you learn how toointegrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4bd28-105">Интеграция пользователей с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4bd28-105">Integrating People with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4bd28-106">Можно управлять в Azure AD, имеющего доступ tooPeople</span><span class="sxs-lookup"><span data-stu-id="4bd28-106">You can control in Azure AD who has access tooPeople</span></span>
- <span data-ttu-id="4bd28-107">Можно включить на пользователей tooautomatically get вошедшего tooPeople (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd28-107">You can enable your users tooautomatically get signed-on tooPeople (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4bd28-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4bd28-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4bd28-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4bd28-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bd28-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4bd28-110">Prerequisites</span></span>

<span data-ttu-id="4bd28-111">tooconfigure интеграция Azure AD с людьми, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4bd28-111">tooconfigure Azure AD integration with People, you need hello following items:</span></span>

- <span data-ttu-id="4bd28-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4bd28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4bd28-113">подписка People с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4bd28-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4bd28-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4bd28-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4bd28-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4bd28-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4bd28-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4bd28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4bd28-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4bd28-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4bd28-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4bd28-118">Scenario description</span></span>
<span data-ttu-id="4bd28-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4bd28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4bd28-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4bd28-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4bd28-121">Добавлении пользователей из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4bd28-121">Adding People from hello gallery</span></span>
2. <span data-ttu-id="4bd28-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd28-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-hello-gallery"></a><span data-ttu-id="4bd28-123">Добавлении пользователей из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4bd28-123">Adding People from hello gallery</span></span>
<span data-ttu-id="4bd28-124">tooconfigure hello интеграция людей в Azure AD, вы должны tooadd людей из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4bd28-124">tooconfigure hello integration of People into Azure AD, you need tooadd People from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4bd28-125">**tooadd людей из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4bd28-125">**tooadd People from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd28-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4bd28-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4bd28-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4bd28-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4bd28-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4bd28-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4bd28-133">Введите в поле поиска hello **людей**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-133">In hello search box, type **People**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="4bd28-135">В панели результатов hello выберите **людей**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4bd28-135">In hello results panel, select **People**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4bd28-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd28-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4bd28-138">В этом разделе описана настройка и проверка единого входа Azure AD в People с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4bd28-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4bd28-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в людей является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4bd28-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in People is tooa user in Azure AD.</span></span> <span data-ttu-id="4bd28-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в пользователей должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4bd28-140">In other words, a link relationship between an Azure AD user and hello related user in People needs toobe established.</span></span>

<span data-ttu-id="4bd28-141">В людей, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4bd28-141">In People, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4bd28-142">tooconfigure и тестирования Azure AD единого входа с пользователями, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4bd28-142">tooconfigure and test Azure AD single sign-on with People, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4bd28-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4bd28-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4bd28-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4bd28-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4bd28-145">**[Создание тестового пользователя людей](#creating-a-people-test-user)**  -toohave аналог Саймон Britta в людей, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4bd28-145">**[Creating a People test user](#creating-a-people-test-user)** - toohave a counterpart of Britta Simon in People that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4bd28-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4bd28-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4bd28-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4bd28-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4bd28-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd28-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4bd28-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа для пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="4bd28-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="4bd28-150">**tooconfigure Azure AD единого входа с пользователями, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4bd28-150">**tooconfigure Azure AD single sign-on with People, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd28-151">В hello в hello портала Azure **людей** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-151">In hello Azure portal, on hello **People** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4bd28-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4bd28-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="4bd28-155">На hello **пользователей домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4bd28-155">On hello **People Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="4bd28-157">а.</span><span class="sxs-lookup"><span data-stu-id="4bd28-157">a.</span></span> <span data-ttu-id="4bd28-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="4bd28-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="4bd28-159">b.</span><span class="sxs-lookup"><span data-stu-id="4bd28-159">b.</span></span> <span data-ttu-id="4bd28-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="4bd28-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="4bd28-161">c.</span><span class="sxs-lookup"><span data-stu-id="4bd28-161">c.</span></span> <span data-ttu-id="4bd28-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="4bd28-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4bd28-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="4bd28-163">These values are not real.</span></span> <span data-ttu-id="4bd28-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="4bd28-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4bd28-165">Обратитесь к [службу поддержки пользователей клиента](mailto:customerservices@peoplehr.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="4bd28-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) tooget these values.</span></span>

5. <span data-ttu-id="4bd28-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4bd28-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="4bd28-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4bd28-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4bd28-170">tooget единого входа, настроенному для вашего приложения, необходимо на toosign tooyour клиента пользователей с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4bd28-170">tooget SSO configured for your application, you need toosign-on tooyour People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="4bd28-171">В меню слева hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-171">In hello menu on hello left side, click **Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="4bd28-173">Нажмите **Компания**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-173">Click **Company**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="4bd28-175">На hello **файл метаданных передачи «Единый вход» SAML**, нажмите кнопку **Обзор** tooupload hello скачать файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="4bd28-175">On hello **Upload 'Single Sign On' SAML meta-data file**, click **Browse** tooupload hello downloaded metadata file.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="4bd28-177">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4bd28-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4bd28-178">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4bd28-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4bd28-179">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4bd28-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4bd28-180">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bd28-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="4bd28-181">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd28-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4bd28-183">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4bd28-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd28-184">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4bd28-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4bd28-186">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4bd28-188">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4bd28-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4bd28-190">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4bd28-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4bd28-192">а.</span><span class="sxs-lookup"><span data-stu-id="4bd28-192">a.</span></span> <span data-ttu-id="4bd28-193">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4bd28-194">b.</span><span class="sxs-lookup"><span data-stu-id="4bd28-194">b.</span></span> <span data-ttu-id="4bd28-195">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4bd28-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4bd28-196">c.</span><span class="sxs-lookup"><span data-stu-id="4bd28-196">c.</span></span> <span data-ttu-id="4bd28-197">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4bd28-198">d.</span><span class="sxs-lookup"><span data-stu-id="4bd28-198">d.</span></span> <span data-ttu-id="4bd28-199">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="4bd28-200">Создание тестового пользователя приложения "Люди"</span><span class="sxs-lookup"><span data-stu-id="4bd28-200">Creating a People test user</span></span>

<span data-ttu-id="4bd28-201">В этом разделе описано, как создать пользователя Britta Simon в приложении People.</span><span class="sxs-lookup"><span data-stu-id="4bd28-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="4bd28-202">Работать с [службу поддержки пользователей клиента](mailto:customerservices@peoplehr.com) для добавления пользователей hello в платформе людей hello.</span><span class="sxs-lookup"><span data-stu-id="4bd28-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add hello users in hello People platform.</span></span> <span data-ttu-id="4bd28-203">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="4bd28-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4bd28-204">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4bd28-204">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4bd28-205">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPeople доступа.</span><span class="sxs-lookup"><span data-stu-id="4bd28-205">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeople.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4bd28-207">**tooassign tooPeople Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4bd28-207">**tooassign Britta Simon tooPeople, perform hello following steps:**</span></span>

1. <span data-ttu-id="4bd28-208">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-208">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4bd28-210">В списке приложений hello выберите **людей**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-210">In hello applications list, select **People**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="4bd28-212">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-212">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4bd28-214">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-214">Click **Add** button.</span></span> <span data-ttu-id="4bd28-215">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4bd28-217">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4bd28-217">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4bd28-218">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4bd28-219">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4bd28-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4bd28-220">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4bd28-220">Testing single sign-on</span></span>

<span data-ttu-id="4bd28-221">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="4bd28-221">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4bd28-222">При нажатии кнопки приветствия людей плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="4bd28-222">When you click hello People tile in hello Access Panel, you should get automatically signed-on tooyour People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4bd28-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4bd28-223">Additional resources</span></span>

* [<span data-ttu-id="4bd28-224">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4bd28-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4bd28-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4bd28-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

