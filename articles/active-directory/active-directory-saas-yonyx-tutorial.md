---
title: "Руководство по интеграции Azure Active Directory с Yonyx Interactive Guides | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Yonyx интерактивного руководства."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="e03b3-103">Руководство по интеграции Azure Active Directory с Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="e03b3-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="e03b3-104">В этом учебнике вы узнаете, как toointegrate Yonyx Interactive проводит в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e03b3-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e03b3-105">Интеграция интерактивных руководств Yonyx с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e03b3-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e03b3-106">Можно управлять в Azure AD, имеющего доступ tooYonyx интерактивного руководства</span><span class="sxs-lookup"><span data-stu-id="e03b3-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="e03b3-107">Ваш пользователей tooautomatically get вошедшего tooYonyx интерактивного руководства (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="e03b3-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e03b3-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e03b3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e03b3-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e03b3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e03b3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e03b3-110">Prerequisites</span></span>

<span data-ttu-id="e03b3-111">tooconfigure интеграция Azure AD с помощью интерактивного руководства Yonyx требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e03b3-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="e03b3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e03b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e03b3-113">подписка Yonyx Interactive Guides с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e03b3-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e03b3-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e03b3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e03b3-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e03b3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e03b3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e03b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e03b3-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e03b3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e03b3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e03b3-118">Scenario description</span></span>
<span data-ttu-id="e03b3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e03b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e03b3-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e03b3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e03b3-121">Добавление интерактивных руководств Yonyx из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e03b3-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="e03b3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e03b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="e03b3-123">Добавление интерактивных руководств Yonyx из галереи hello</span><span class="sxs-lookup"><span data-stu-id="e03b3-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="e03b3-124">tooconfigure hello интеграция интерактивных руководств Yonyx в Azure AD, вы должны tooadd Yonyx интерактивного руководства из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e03b3-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e03b3-125">**tooadd Yonyx интерактивного руководства из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="e03b3-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e03b3-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e03b3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="e03b3-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e03b3-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="e03b3-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e03b3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="e03b3-133">Введите в поле поиска hello **Yonyx интерактивного руководства**выберите **Yonyx интерактивных руководств** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e03b3-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Yonyx интерактивных руководств в списке результатов hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e03b3-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e03b3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e03b3-136">В этом разделе описана настройка и проверка единого входа Azure AD в Yonyx Interactive Guides с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e03b3-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e03b3-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в интерактивных руководств Yonyx является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e03b3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="e03b3-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в интерактивных руководств Yonyx должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e03b3-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="e03b3-139">В руководствах по интерактивной Yonyx, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e03b3-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e03b3-140">tooconfigure и тестирования Azure AD единого входа с помощью интерактивного руководства Yonyx, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e03b3-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e03b3-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e03b3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e03b3-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e03b3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e03b3-143">**[Создание тестового пользователя интерактивных руководств Yonyx](#create-a-yonyx-interactive-guides-test-user)**  -toohave аналог Саймон Britta Yonyx интерактивных руководств, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e03b3-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e03b3-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e03b3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e03b3-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e03b3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e03b3-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e03b3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e03b3-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Yonyx интерактивного руководства.</span><span class="sxs-lookup"><span data-stu-id="e03b3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="e03b3-148">**tooconfigure Azure AD единого входа с помощью интерактивного руководства Yonyx, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e03b3-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="e03b3-149">В hello в hello портала Azure **интерактивных руководств Yonyx** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e03b3-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e03b3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="e03b3-153">На hello **Yonyx интерактивного руководства домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e03b3-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="e03b3-155">а.</span><span class="sxs-lookup"><span data-stu-id="e03b3-155">a.</span></span> <span data-ttu-id="e03b3-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="e03b3-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="e03b3-157">b.</span><span class="sxs-lookup"><span data-stu-id="e03b3-157">b.</span></span> <span data-ttu-id="e03b3-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="e03b3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e03b3-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e03b3-159">These values are not real.</span></span> <span data-ttu-id="e03b3-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e03b3-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e03b3-161">Обратитесь к [Yonyx интерактивного руководства клиента поддержки](mailto:support@yonyx.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="e03b3-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="e03b3-162">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e03b3-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="e03b3-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e03b3-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e03b3-166">На hello **Yonyx интерактивного руководства по конфигурации** щелкните **настройки интерактивного руководства Yonyx** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e03b3-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e03b3-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e03b3-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="e03b3-169">tooconfigure единого входа на **интерактивных руководств Yonyx** стороны, необходимо загрузить hello toosend **Certificate(Base64)**, **URL-адрес выхода**, **SAML Single Sign On URL-адрес службы** **идентификатор сущности SAML** слишком[Yonyx интерактивных руководств поддержки](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="e03b3-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="e03b3-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="e03b3-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e03b3-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e03b3-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e03b3-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e03b3-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e03b3-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e03b3-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e03b3-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e03b3-174">Create an Azure AD test user</span></span>

<span data-ttu-id="e03b3-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e03b3-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="e03b3-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e03b3-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e03b3-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e03b3-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e03b3-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e03b3-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="e03b3-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e03b3-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e03b3-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e03b3-186">а.</span><span class="sxs-lookup"><span data-stu-id="e03b3-186">a.</span></span> <span data-ttu-id="e03b3-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e03b3-188">b.</span><span class="sxs-lookup"><span data-stu-id="e03b3-188">b.</span></span> <span data-ttu-id="e03b3-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e03b3-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e03b3-190">c.</span><span class="sxs-lookup"><span data-stu-id="e03b3-190">c.</span></span> <span data-ttu-id="e03b3-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e03b3-192">d.</span><span class="sxs-lookup"><span data-stu-id="e03b3-192">d.</span></span> <span data-ttu-id="e03b3-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="e03b3-194">Создание тестового пользователя Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="e03b3-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="e03b3-195">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Yonyx интерактивных руководств.</span><span class="sxs-lookup"><span data-stu-id="e03b3-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="e03b3-196">Приложение Yonyx Interactive Guides поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e03b3-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e03b3-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="e03b3-197">There is no action item for you in this section.</span></span> <span data-ttu-id="e03b3-198">Новый пользователь создается во время попытки tooaccess Yonyx интерактивных руководств, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e03b3-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e03b3-199">При необходимости toocreate пользователя вручную, необходимо toocontact hello интерактивных руководств Yonyx поддержки через < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="e03b3-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e03b3-200">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e03b3-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e03b3-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooYonyx интерактивного руководства.</span><span class="sxs-lookup"><span data-stu-id="e03b3-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="e03b3-203">**tooassign Britta Simon tooYonyx интерактивного руководства, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="e03b3-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="e03b3-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e03b3-206">В списке приложений hello выберите **Yonyx интерактивного руководства**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![ссылка интерактивного руководства Yonyx Hello в списке приложений hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="e03b3-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="e03b3-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-210">Click **Add** button.</span></span> <span data-ttu-id="e03b3-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="e03b3-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e03b3-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e03b3-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e03b3-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e03b3-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e03b3-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e03b3-216">Test single sign-on</span></span>

<span data-ttu-id="e03b3-217">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="e03b3-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e03b3-218">При нажатии кнопки приветствия интерактивных руководств Yonyx плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения Yonyx интерактивного руководства.</span><span class="sxs-lookup"><span data-stu-id="e03b3-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="e03b3-219">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e03b3-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e03b3-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e03b3-220">Additional resources</span></span>

* [<span data-ttu-id="e03b3-221">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e03b3-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e03b3-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e03b3-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

