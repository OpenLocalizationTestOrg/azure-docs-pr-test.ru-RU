---
title: "Руководство по интеграции Azure Active Directory с Predictix Assortment Planning | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и планирования ассортимента Predictix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1294b712caf12fdafaf65d70a02ee9fbdc3e84a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="2ceaa-103">Руководство. Интеграция Azure Active Directory с Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="2ceaa-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="2ceaa-104">В этом учебнике вы узнаете, как toointegrate Predictix планирования ассортимента с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-104">In this tutorial, you learn how toointegrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ceaa-105">Интеграция с Azure AD планирования ассортимента Predictix предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-105">Integrating Predictix Assortment Planning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ceaa-106">Можно управлять в Azure AD, имеющего доступ tooPredictix планирования ассортимента.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-106">You can control in Azure AD who has access tooPredictix Assortment Planning.</span></span>
- <span data-ttu-id="2ceaa-107">Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooPredictix планирования ассортимента (Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-107">You can enable your users tooautomatically get signed-on tooPredictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2ceaa-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2ceaa-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ceaa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2ceaa-110">Prerequisites</span></span>

<span data-ttu-id="2ceaa-111">tooconfigure интеграция Azure AD с планирования ассортимента Predictix требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-111">tooconfigure Azure AD integration with Predictix Assortment Planning, you need hello following items:</span></span>

- <span data-ttu-id="2ceaa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2ceaa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ceaa-113">подписка на Predictix Assortment Planning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ceaa-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ceaa-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ceaa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ceaa-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ceaa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2ceaa-118">Scenario description</span></span>
<span data-ttu-id="2ceaa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ceaa-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ceaa-121">Добавление планирования ассортимента Predictix из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2ceaa-121">Adding Predictix Assortment Planning from hello gallery</span></span>
2. <span data-ttu-id="2ceaa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ceaa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-hello-gallery"></a><span data-ttu-id="2ceaa-123">Добавление планирования ассортимента Predictix из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2ceaa-123">Adding Predictix Assortment Planning from hello gallery</span></span>
<span data-ttu-id="2ceaa-124">tooconfigure hello интеграция Predictix ассортимент планирования в Azure AD, вы должны tooadd планирования ассортимента Predictix из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-124">tooconfigure hello integration of Predictix Assortment Planning into Azure AD, you need tooadd Predictix Assortment Planning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ceaa-125">**tooadd Predictix планирования ассортимента из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="2ceaa-125">**tooadd Predictix Assortment Planning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ceaa-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="2ceaa-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ceaa-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="2ceaa-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="2ceaa-133">Введите в поле поиска hello **планирования ассортимента Predictix**выберите **планирования ассортимента Predictix** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-133">In hello search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix ассортимент планирования в списке результатов hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2ceaa-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ceaa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2ceaa-136">В этом разделе описана настройка и проверка единого входа Azure AD в Predictix Assortment Planning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2ceaa-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в планировании ассортимент Predictix является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Assortment Planning is tooa user in Azure AD.</span></span> <span data-ttu-id="2ceaa-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в планировании ассортимент Predictix должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Assortment Planning needs toobe established.</span></span>

<span data-ttu-id="2ceaa-139">При планировании ассортимент Predictix, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-139">In Predictix Assortment Planning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ceaa-140">tooconfigure и теста Azure AD единого входа с Predictix ассортимент планирования, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-140">tooconfigure and test Azure AD single sign-on with Predictix Assortment Planning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ceaa-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ceaa-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ceaa-143">**[Создание тестового пользователя планирования ассортимента Predictix](#create-a-predictix-assortment-planning-test-user)**  -toohave аналог Саймон Britta Predictix ассортимент планирования, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - toohave a counterpart of Britta Simon in Predictix Assortment Planning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ceaa-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ceaa-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2ceaa-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ceaa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2ceaa-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение планирования ассортимента Predictix.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="2ceaa-148">**tooconfigure Azure AD единого входа с Predictix ассортимент планирования, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2ceaa-148">**tooconfigure Azure AD single sign-on with Predictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ceaa-149">В hello в hello портала Azure **планирования ассортимента Predictix** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-149">In hello Azure portal, on hello **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="2ceaa-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="2ceaa-153">На hello **URL-адреса и домена планирования ассортимента Predictix** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-153">On hello **Predictix Assortment Planning Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="2ceaa-155">а.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-155">a.</span></span> <span data-ttu-id="2ceaa-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="2ceaa-157">b.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-157">b.</span></span> <span data-ttu-id="2ceaa-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="2ceaa-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-159">These values are not real.</span></span> <span data-ttu-id="2ceaa-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2ceaa-161">Обратитесь к [группа поддержки клиента планирования ассортимента Predictix](http://www.infor.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) tooget these values.</span></span> 
 


4. <span data-ttu-id="2ceaa-162">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="2ceaa-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2ceaa-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ceaa-166">На hello **Predictix ассортимент Планирование конфигурации** щелкните **Настройка планирования ассортимента Predictix** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-166">On hello **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ceaa-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="2ceaa-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="2ceaa-169">tooconfigure единого входа на **планирования ассортимента Predictix** стороны, необходимо загрузить hello toosend **Certificate(Base64)**, **идентификатор сущности SAML**,  **SAML единого входа URL-адрес службы**, и **URL-адрес выхода** слишком[Predictix ассортимент Планирование поддержки](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-169">tooconfigure single sign-on on **Predictix Assortment Planning** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  too[Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="2ceaa-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2ceaa-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="2ceaa-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ceaa-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ceaa-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ceaa-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2ceaa-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ceaa-174">Create an Azure AD test user</span></span>

<span data-ttu-id="2ceaa-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="2ceaa-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2ceaa-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ceaa-178">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2ceaa-180">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2ceaa-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2ceaa-184">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2ceaa-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2ceaa-186">а.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-186">a.</span></span> <span data-ttu-id="2ceaa-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ceaa-188">b.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-188">b.</span></span> <span data-ttu-id="2ceaa-189">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2ceaa-190">c.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-190">c.</span></span> <span data-ttu-id="2ceaa-191">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2ceaa-192">d.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-192">d.</span></span> <span data-ttu-id="2ceaa-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="2ceaa-194">Создание тестового пользователя Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="2ceaa-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="2ceaa-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="2ceaa-196">Можно работать с [Predictix ассортимент Планирование поддержки](http://www.infor.com/contact/) tooadd пользователей hello в платформу планирования ассортимента Predictix hello.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) tooadd hello users in hello Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="2ceaa-197">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-197">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2ceaa-198">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2ceaa-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2ceaa-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooPredictix планирования ассортимента.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Assortment Planning.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="2ceaa-201">**tooassign tooPredictix Britta Simon ассортимент планирования, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="2ceaa-201">**tooassign Britta Simon tooPredictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ceaa-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2ceaa-204">В списке приложений hello выберите **планирования ассортимента Predictix**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-204">In hello applications list, select **Predictix Assortment Planning**.</span></span>

    ![Hello планирования ассортимента Predictix ссылку в списке приложений hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="2ceaa-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="2ceaa-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-208">Click **Add** button.</span></span> <span data-ttu-id="2ceaa-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="2ceaa-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ceaa-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ceaa-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2ceaa-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2ceaa-214">Test single sign-on</span></span>

<span data-ttu-id="2ceaa-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ceaa-216">При нажатии кнопки hello планирования ассортимента Predictix плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour планирования ассортимента Predictix приложения.</span><span class="sxs-lookup"><span data-stu-id="2ceaa-216">When you click hello Predictix Assortment Planning tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Assortment Planning application.</span></span>
<span data-ttu-id="2ceaa-217">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ceaa-217">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2ceaa-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2ceaa-218">Additional resources</span></span>

* [<span data-ttu-id="2ceaa-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ceaa-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ceaa-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2ceaa-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

