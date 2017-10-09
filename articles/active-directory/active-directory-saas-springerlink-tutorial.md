---
title: "Руководство по интеграции Azure Active Directory с приложением Springer Link | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Springer ссылку."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="d1a60-103">Руководство: интеграция Azure Active Directory с Springer Link</span><span class="sxs-lookup"><span data-stu-id="d1a60-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="d1a60-104">В этом учебнике вы узнаете, как toointegrate Springer компоновку с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1a60-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1a60-105">Интеграция Springer связи с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d1a60-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d1a60-106">Можно управлять в Azure AD, имеющего доступ tooSpringer ссылку.</span><span class="sxs-lookup"><span data-stu-id="d1a60-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="d1a60-107">Вы можете включить вашей пользователей tooautomatically get вошедшего tooSpringer связи (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1a60-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d1a60-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a60-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d1a60-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1a60-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1a60-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d1a60-110">Prerequisites</span></span>

<span data-ttu-id="d1a60-111">tooconfigure интеграция Azure AD с помощью ссылки Springer требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d1a60-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="d1a60-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d1a60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1a60-113">подписка Springer Link с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d1a60-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1a60-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d1a60-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1a60-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d1a60-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1a60-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d1a60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1a60-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1a60-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1a60-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d1a60-118">Scenario description</span></span>
<span data-ttu-id="d1a60-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d1a60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1a60-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d1a60-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1a60-121">Добавление ссылки Springer из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d1a60-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="d1a60-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1a60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="d1a60-123">Добавление ссылки Springer из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d1a60-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="d1a60-124">tooconfigure hello интеграции Springer ссылку в Azure AD, вы должны tooadd Springer ссылку из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d1a60-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d1a60-125">**tooadd Springer ссылку из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="d1a60-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1a60-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d1a60-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="d1a60-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d1a60-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="d1a60-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d1a60-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="d1a60-133">Введите в поле поиска hello **Springer ссылку**выберите **Springer ссылку** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d1a60-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Springer ссылку в списке результатов hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d1a60-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1a60-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d1a60-136">В этом разделе описана настройка и проверка единого входа Azure AD в Springer Link с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1a60-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1a60-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ссылке Springer является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1a60-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="d1a60-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ссылке Springer должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d1a60-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="d1a60-139">В ссылке Springer, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d1a60-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d1a60-140">tooconfigure и теста Azure AD единого входа с Springer ссылку, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d1a60-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d1a60-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d1a60-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d1a60-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d1a60-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1a60-143">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d1a60-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="d1a60-144">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d1a60-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d1a60-145">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1a60-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d1a60-146">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Springer ссылку.</span><span class="sxs-lookup"><span data-stu-id="d1a60-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="d1a60-147">**tooconfigure Azure AD единого входа с помощью ссылки Springer выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d1a60-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1a60-148">В hello в hello портала Azure **ссылку Springer** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="d1a60-150">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d1a60-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="d1a60-152">На hello **Springer связи домена и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="d1a60-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="d1a60-154">а.</span><span class="sxs-lookup"><span data-stu-id="d1a60-154">a.</span></span> <span data-ttu-id="d1a60-155">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="d1a60-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="d1a60-156">b.</span><span class="sxs-lookup"><span data-stu-id="d1a60-156">b.</span></span> <span data-ttu-id="d1a60-157">В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d1a60-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="d1a60-158">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="d1a60-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d1a60-159">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="d1a60-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="d1a60-161">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d1a60-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="d1a60-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d1a60-162">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1a60-164">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d1a60-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="d1a60-165">а.</span><span class="sxs-lookup"><span data-stu-id="d1a60-165">a.</span></span> <span data-ttu-id="d1a60-166">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-166">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="d1a60-168">b.</span><span class="sxs-lookup"><span data-stu-id="d1a60-168">b.</span></span> <span data-ttu-id="d1a60-169">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d1a60-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="d1a60-171">c.</span><span class="sxs-lookup"><span data-stu-id="d1a60-171">c.</span></span> <span data-ttu-id="d1a60-172">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="d1a60-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="d1a60-174">d.</span><span class="sxs-lookup"><span data-stu-id="d1a60-174">d.</span></span> <span data-ttu-id="d1a60-175">Теперь перейдите на странице свойств toohello **Springer ссылку** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="d1a60-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="d1a60-177">д.</span><span class="sxs-lookup"><span data-stu-id="d1a60-177">e.</span></span> <span data-ttu-id="d1a60-178">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d1a60-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="d1a60-179">tooconfigure единого входа на **Springer ссылку** стороне необходимо hello toosend создан **URL-адрес метаданных** слишком[Springer ссылку поддержки](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="d1a60-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="d1a60-180">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d1a60-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d1a60-181">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d1a60-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d1a60-182">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1a60-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d1a60-183">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1a60-183">Create an Azure AD test user</span></span>

<span data-ttu-id="d1a60-184">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a60-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="d1a60-186">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d1a60-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1a60-187">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1a60-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d1a60-189">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d1a60-191">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d1a60-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d1a60-193">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d1a60-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d1a60-195">а.</span><span class="sxs-lookup"><span data-stu-id="d1a60-195">a.</span></span> <span data-ttu-id="d1a60-196">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1a60-197">b.</span><span class="sxs-lookup"><span data-stu-id="d1a60-197">b.</span></span> <span data-ttu-id="d1a60-198">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d1a60-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d1a60-199">c.</span><span class="sxs-lookup"><span data-stu-id="d1a60-199">c.</span></span> <span data-ttu-id="d1a60-200">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="d1a60-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d1a60-201">d.</span><span class="sxs-lookup"><span data-stu-id="d1a60-201">d.</span></span> <span data-ttu-id="d1a60-202">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d1a60-203">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d1a60-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d1a60-204">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа к tooSpringer ссылку.</span><span class="sxs-lookup"><span data-stu-id="d1a60-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="d1a60-206">**tooassign tooSpringer Britta Simon ссылку, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="d1a60-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1a60-207">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d1a60-209">В списке приложений hello выберите **Springer ссылку**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-209">In hello applications list, select **Springer Link**.</span></span>

    ![ссылка Springer ссылку Hello в списке приложений hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="d1a60-211">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="d1a60-213">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-213">Click **Add** button.</span></span> <span data-ttu-id="d1a60-214">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="d1a60-216">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d1a60-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d1a60-217">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1a60-218">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d1a60-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d1a60-219">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d1a60-219">Test single sign-on</span></span>

<span data-ttu-id="d1a60-220">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d1a60-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d1a60-221">Если щелкнуть плитку ссылку Springer hello в hello панели доступа, вы должны получить приложения автоматически вошедшего tooyour Springer связи.</span><span class="sxs-lookup"><span data-stu-id="d1a60-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="d1a60-222">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1a60-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1a60-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d1a60-223">Additional resources</span></span>

* [<span data-ttu-id="d1a60-224">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1a60-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1a60-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1a60-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

