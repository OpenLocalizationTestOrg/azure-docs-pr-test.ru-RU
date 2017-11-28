---
title: "Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и единого входа SAML JIRA корпорацией Майкрософт."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="74005-103">Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="74005-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="74005-104">В этом учебнике вы узнаете, как toointegrate единого входа SAML JIRA корпорацией Майкрософт в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74005-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74005-105">Интеграция единого входа SAML JIRA корпорацией Майкрософт с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="74005-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="74005-106">Можно управлять в Azure AD, имеющего доступ tooJIRA единого входа SAML корпорацией Майкрософт</span><span class="sxs-lookup"><span data-stu-id="74005-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="74005-107">Ваш пользователей tooautomatically get вошедшего tooJIRA единого входа SAML корпорацией Майкрософт (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74005-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="74005-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="74005-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74005-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74005-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74005-110">Prerequisites</span></span>

<span data-ttu-id="74005-111">tooconfigure интеграция Azure AD с помощью единого входа SAML JIRA корпорацией Майкрософт, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="74005-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="74005-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="74005-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74005-113">JIRA серверного приложения, установленные на сервере Windows 64-разрядная (локально или в облаке hello инфраструктуры IaaS)</span><span class="sxs-lookup"><span data-stu-id="74005-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="74005-114">поддержка HTTPS на сервере JIRA;</span><span class="sxs-lookup"><span data-stu-id="74005-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="74005-115">Примечание версии hello поддерживается для подключаемого модуля JIRA упоминаются в под разделом.</span><span class="sxs-lookup"><span data-stu-id="74005-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="74005-116">JIRA сервер доступен в Интернете особенно tooAzure входа AD для проверки подлинности и необходимо будет tooreceive hello токена из Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="74005-117">в JIRA должны быть настроены учетные данные администратора;</span><span class="sxs-lookup"><span data-stu-id="74005-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="74005-118">в JIRA должна быть отключена поддержка WebSudo;</span><span class="sxs-lookup"><span data-stu-id="74005-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="74005-119">Тестовый пользователь, созданные в hello JIRA серверного приложения</span><span class="sxs-lookup"><span data-stu-id="74005-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="74005-120">в этом учебнике шаги tootest hello, не рекомендуется использовать рабочей среде JIRA.</span><span class="sxs-lookup"><span data-stu-id="74005-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="74005-121">Сначала протестируйте интеграцию hello в разработки или промежуточной среде приложения hello, а затем используйте hello рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="74005-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="74005-122">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="74005-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74005-123">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="74005-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74005-124">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74005-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="74005-125">Поддерживаемые версии JIRA</span><span class="sxs-lookup"><span data-stu-id="74005-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="74005-126">Сейчас поддерживаются следующие версии JIRA:</span><span class="sxs-lookup"><span data-stu-id="74005-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="74005-127">Ядро JIRA и программного обеспечения: 6.0 too7.2.0</span><span class="sxs-lookup"><span data-stu-id="74005-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="74005-128">JIRA службы поддержки: 3.0 too3.2</span><span class="sxs-lookup"><span data-stu-id="74005-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74005-129">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="74005-129">Scenario description</span></span>
<span data-ttu-id="74005-130">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="74005-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74005-131">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="74005-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74005-132">Добавление единого входа SAML JIRA корпорацией Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="74005-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="74005-133">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="74005-134">Добавление единого входа SAML JIRA корпорацией Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="74005-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="74005-135">tooconfigure hello интеграции единого входа SAML JIRA корпорацией Майкрософт в Azure AD, вы должны tooadd единого входа SAML JIRA корпорацией Майкрософт из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="74005-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="74005-136">**tooadd единого входа SAML JIRA корпорацией Майкрософт из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="74005-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="74005-137">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="74005-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74005-139">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="74005-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="74005-140">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="74005-140">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="74005-142">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="74005-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="74005-144">Введите в поле поиска hello **JIRA единого входа SAML корпорацией Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="74005-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="74005-146">В панели результатов hello выберите **JIRA единого входа SAML корпорацией Майкрософт**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="74005-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74005-148">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74005-149">В этом разделе описана настройка и проверка единого входа Azure AD в JIRA SAML SSO by Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74005-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="74005-150">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в единый вход SAML JIRA корпорацией Майкрософт является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74005-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="74005-151">Другими словами связи между пользователя Azure AD и связанных пользователей hello в единый вход SAML JIRA корпорацией Майкрософт должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="74005-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="74005-152">В единый вход SAML JIRA корпорацией Майкрософт, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="74005-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="74005-153">tooconfigure и тестирования Azure AD единого входа с помощью единого входа SAML JIRA корпорацией Майкрософт, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="74005-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="74005-154">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="74005-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="74005-155">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="74005-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74005-156">**[Создание единого входа SAML JIRA теста пользователем Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave аналог Саймон Britta в единый вход SAML JIRA корпорацией Майкрософт, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="74005-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="74005-157">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="74005-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74005-158">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="74005-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74005-159">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74005-160">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш единого входа SAML JIRA приложением Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74005-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="74005-161">**tooconfigure Azure AD единого входа с помощью единого входа SAML JIRA корпорацией Майкрософт, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="74005-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="74005-162">В hello в hello портала Azure **JIRA единого входа SAML корпорацией Майкрософт** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="74005-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="74005-164">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="74005-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="74005-166">На hello **JIRA единого входа SAML, URL-адреса и домена Microsoft** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="74005-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="74005-168">а.</span><span class="sxs-lookup"><span data-stu-id="74005-168">a.</span></span> <span data-ttu-id="74005-169">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="74005-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="74005-170">b.</span><span class="sxs-lookup"><span data-stu-id="74005-170">b.</span></span> <span data-ttu-id="74005-171">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="74005-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="74005-172">c.</span><span class="sxs-lookup"><span data-stu-id="74005-172">c.</span></span> <span data-ttu-id="74005-173">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="74005-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74005-174">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="74005-174">These values are not real.</span></span> <span data-ttu-id="74005-175">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="74005-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="74005-176">Если это именованный URL-адрес, то порт указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="74005-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="74005-177">Эти значения будут получены во время настройки hello Jira подключаемого модуля, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="74005-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="74005-178">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="74005-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="74005-179">а.</span><span class="sxs-lookup"><span data-stu-id="74005-179">a.</span></span> <span data-ttu-id="74005-180">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="74005-180">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="74005-182">b.</span><span class="sxs-lookup"><span data-stu-id="74005-182">b.</span></span> <span data-ttu-id="74005-183">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="74005-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="74005-185">c.</span><span class="sxs-lookup"><span data-stu-id="74005-185">c.</span></span> <span data-ttu-id="74005-186">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="74005-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="74005-188">d.</span><span class="sxs-lookup"><span data-stu-id="74005-188">d.</span></span> <span data-ttu-id="74005-189">Теперь перейдите на странице свойств toohello **JIRA единого входа SAML корпорацией Майкрософт** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="74005-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="74005-191">д.</span><span class="sxs-lookup"><span data-stu-id="74005-191">e.</span></span> <span data-ttu-id="74005-192">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` и скопируйте это значение в блокноте, как используется позднее для конфигурации hello hello подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="74005-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="74005-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="74005-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="74005-195">Обратитесь к [Microsoft](mailto:waadpartners@microsoft.com) с hello следующую информацию для подключаемого модуля JIRA hello.</span><span class="sxs-lookup"><span data-stu-id="74005-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="74005-196">Имя клиента:</span><span class="sxs-lookup"><span data-stu-id="74005-196">Customer Name:</span></span>
    *   <span data-ttu-id="74005-197">Основное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="74005-197">Primary domain name:</span></span>
    *   <span data-ttu-id="74005-198">Azure AD Premium: Да/Нет (подключаемого модуля будут доступны tooall hello клиента Free, Basic и Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="74005-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="74005-199">Число пользователей, которые будут использовать данную интеграцию:</span><span class="sxs-lookup"><span data-stu-id="74005-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="74005-200">версия JIRA;</span><span class="sxs-lookup"><span data-stu-id="74005-200">JIRA Version:</span></span>
    *   <span data-ttu-id="74005-201">Комментарии.</span><span class="sxs-lookup"><span data-stu-id="74005-201">Comments:</span></span>

7. <span data-ttu-id="74005-202">В другом окне браузера войдите в экземпляр JIRA tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="74005-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="74005-203">Наведите указатель мыши на шестеренки и выберите hello **надстройки**.</span><span class="sxs-lookup"><span data-stu-id="74005-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="74005-205">На вкладке "Надстройки" щелкните **Управление надстройками**.</span><span class="sxs-lookup"><span data-stu-id="74005-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="74005-207">Вручную Загрузите подключаемый модуль hello, предоставляемых корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="74005-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="74005-208">Если установлен подключаемый модуль hello, оно появляется в **пользователь установил** надстройки раздел **Управление надстройками** раздела.</span><span class="sxs-lookup"><span data-stu-id="74005-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="74005-209">Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="74005-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="74005-210">Выполните следующие действия на странице настройки:</span><span class="sxs-lookup"><span data-stu-id="74005-210">Perform following steps on configuration page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="74005-212">а.</span><span class="sxs-lookup"><span data-stu-id="74005-212">a.</span></span> <span data-ttu-id="74005-213">В **URL-адрес метаданных** вставьте hello **URL-адрес метаданных** создаются из Azure AD и щелкните hello **Разрешить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74005-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="74005-214">Считывает URL-адрес метаданных поставщика удостоверений hello и заполняет все сведения о полях hello.</span><span class="sxs-lookup"><span data-stu-id="74005-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="74005-215">По умолчанию идентификатор пользователя SAML указан в идентификаторе имени.</span><span class="sxs-lookup"><span data-stu-id="74005-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="74005-216">Можно изменить этот параметр tooan атрибута и введите имя соответствующего атрибута hello.</span><span class="sxs-lookup"><span data-stu-id="74005-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="74005-217">Убедитесь, что имеется только один сертификат, сопоставленных с приложение hello, таким образом, не содержит ошибок в разрешении метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="74005-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="74005-218">Если имеется несколько сертификатов, при разрешении метаданных hello admin возвращает ошибку.</span><span class="sxs-lookup"><span data-stu-id="74005-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="74005-219">b.</span><span class="sxs-lookup"><span data-stu-id="74005-219">b.</span></span> <span data-ttu-id="74005-220">Копировать hello **идентификатор, URL-адрес ответа и URL-адрес входа** значения и вставьте их в **идентификатор, URL-адрес ответа и URL-адрес входа** соответственно, в текстовых полях **единого входа SAML JIRA доменом Microsoft и URL-адреса** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="74005-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="74005-221">c.</span><span class="sxs-lookup"><span data-stu-id="74005-221">c.</span></span> <span data-ttu-id="74005-222">В **имя кнопки входа** имя типа hello кнопки организация хочет hello toosee пользователей на экране входа.</span><span class="sxs-lookup"><span data-stu-id="74005-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="74005-223">d.</span><span class="sxs-lookup"><span data-stu-id="74005-223">d.</span></span> <span data-ttu-id="74005-224">В **размещение идентификатора пользователя SAML** выберите либо **идентификатор пользователя находится в элементе NameIdentifier hello hello оператора Subject** или **идентификатор пользователя — это элемент атрибута**.</span><span class="sxs-lookup"><span data-stu-id="74005-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="74005-225">Этот идентификатор имеет идентификатор пользователя JIRA toobe hello. Если идентификатор пользователя hello нет соответствия, система не позволит пользователям toolog в.</span><span class="sxs-lookup"><span data-stu-id="74005-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="74005-226">д.</span><span class="sxs-lookup"><span data-stu-id="74005-226">e.</span></span> <span data-ttu-id="74005-227">При выборе **идентификатор пользователя — это элемент атрибута** параметр, а затем в **имя атрибута** текстовое поле типа hello имя атрибута hello, где ожидается идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="74005-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="74005-228">f.</span><span class="sxs-lookup"><span data-stu-id="74005-228">f.</span></span> <span data-ttu-id="74005-229">При использовании hello федеративного домена (например, служб федерации Active Directory и т.д.) в Azure AD выберите команду hello **включения обнаружения домашней области** и настройте hello **доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="74005-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="74005-230">ж.</span><span class="sxs-lookup"><span data-stu-id="74005-230">g.</span></span> <span data-ttu-id="74005-231">В **доменное имя** типа hello доменное имя здесь в случае входа на основе ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="74005-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="74005-232">h.</span><span class="sxs-lookup"><span data-stu-id="74005-232">h.</span></span> <span data-ttu-id="74005-233">Проверьте **Включить единый Выход** при необходимости toolog out из Azure AD, когда пользователь выполняет выход из JIRA.</span><span class="sxs-lookup"><span data-stu-id="74005-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="74005-234">i.</span><span class="sxs-lookup"><span data-stu-id="74005-234">i.</span></span> <span data-ttu-id="74005-235">Нажмите кнопку **Сохранить** кнопку Параметры toosave hello.</span><span class="sxs-lookup"><span data-stu-id="74005-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="74005-236">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="74005-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="74005-237">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="74005-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="74005-238">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74005-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74005-239">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="74005-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="74005-240">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="74005-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="74005-242">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="74005-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="74005-243">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="74005-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74005-245">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="74005-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74005-247">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="74005-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74005-249">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="74005-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74005-251">а.</span><span class="sxs-lookup"><span data-stu-id="74005-251">a.</span></span> <span data-ttu-id="74005-252">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74005-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74005-253">b.</span><span class="sxs-lookup"><span data-stu-id="74005-253">b.</span></span> <span data-ttu-id="74005-254">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="74005-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74005-255">c.</span><span class="sxs-lookup"><span data-stu-id="74005-255">c.</span></span> <span data-ttu-id="74005-256">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="74005-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="74005-257">d.</span><span class="sxs-lookup"><span data-stu-id="74005-257">d.</span></span> <span data-ttu-id="74005-258">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="74005-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="74005-259">Создание тестового пользователя JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="74005-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="74005-260">Пользователи toolog tooenable Azure AD в tooJIRA на локальном сервере, их необходимо подготовить в единый вход SAML JIRA корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="74005-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="74005-261">Для JIRA SAML SSO by Microsoft подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="74005-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="74005-262">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="74005-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="74005-263">Войдите в tooyour JIRA локального сервера с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="74005-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="74005-264">Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="74005-264">Hover on cog and click hello **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="74005-266">Являются tooenter страницы доступ перенаправленной tooAdministrator **пароль** и нажмите кнопку **Подтверждение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74005-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="74005-268">В разделе **User management** (Управление пользователями) щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="74005-268">Under **User management** tab section, click **create user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="74005-270">На hello **«Создать пользователя»** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="74005-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="74005-272">а.</span><span class="sxs-lookup"><span data-stu-id="74005-272">a.</span></span> <span data-ttu-id="74005-273">В hello **адрес электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="74005-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="74005-274">b.</span><span class="sxs-lookup"><span data-stu-id="74005-274">b.</span></span> <span data-ttu-id="74005-275">В hello **полное имя** текстовое поле, полное имя типа пользователя hello как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="74005-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="74005-276">c.</span><span class="sxs-lookup"><span data-stu-id="74005-276">c.</span></span> <span data-ttu-id="74005-277">В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="74005-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="74005-278">d.</span><span class="sxs-lookup"><span data-stu-id="74005-278">d.</span></span> <span data-ttu-id="74005-279">В hello **пароль** текстового поля, типа hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="74005-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="74005-280">д.</span><span class="sxs-lookup"><span data-stu-id="74005-280">e.</span></span> <span data-ttu-id="74005-281">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="74005-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="74005-282">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="74005-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="74005-283">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooJIRA единого входа SAML корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="74005-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="74005-285">**tooassign tooJIRA Britta Simon единого входа SAML корпорацией Майкрософт, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="74005-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="74005-286">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="74005-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="74005-288">В списке приложений hello выберите **JIRA единого входа SAML корпорацией Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="74005-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="74005-290">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="74005-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="74005-292">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74005-292">Click **Add** button.</span></span> <span data-ttu-id="74005-293">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="74005-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="74005-295">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="74005-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="74005-296">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="74005-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74005-297">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="74005-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="74005-298">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="74005-298">Testing single sign-on</span></span>

<span data-ttu-id="74005-299">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="74005-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="74005-300">При нажатии кнопки hello единого входа SAML JIRA по Microsoft плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour единого входа SAML JIRA приложением Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74005-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="74005-301">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="74005-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74005-302">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="74005-302">Additional resources</span></span>

* [<span data-ttu-id="74005-303">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74005-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74005-304">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74005-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

