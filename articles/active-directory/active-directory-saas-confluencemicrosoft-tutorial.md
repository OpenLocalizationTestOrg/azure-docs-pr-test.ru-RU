---
title: "Руководство по интеграции Azure Active Directory с Confluence SAML SSO by Microsoft | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и единого входа SAML является точка пересечения корпорацией Майкрософт."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="bacfc-103">Руководство по интеграции Azure Active Directory с Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="bacfc-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="bacfc-104">В этом учебнике вы узнаете, как toointegrate единого входа SAML является точка пересечения корпорацией Майкрософт в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bacfc-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bacfc-105">Интеграция единого входа SAML является точка пересечения корпорацией Майкрософт с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bacfc-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bacfc-106">Можно управлять в Azure AD, имеющего доступ tooConfluence единого входа SAML корпорацией Майкрософт</span><span class="sxs-lookup"><span data-stu-id="bacfc-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="bacfc-107">Ваш пользователей tooautomatically get вошедшего tooConfluence единого входа SAML корпорацией Майкрософт (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bacfc-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bacfc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bacfc-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bacfc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bacfc-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bacfc-110">Prerequisites</span></span>

<span data-ttu-id="bacfc-111">tooconfigure интеграция Azure AD с помощью единого входа SAML является точка пересечения корпорацией Майкрософт, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bacfc-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="bacfc-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bacfc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bacfc-113">Является точка пересечения серверного приложения, установленные на сервере Windows 64-разрядная (локально или в облаке hello инфраструктуры IaaS)</span><span class="sxs-lookup"><span data-stu-id="bacfc-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="bacfc-114">поддержка HTTPS на сервере Confluence;</span><span class="sxs-lookup"><span data-stu-id="bacfc-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="bacfc-115">Примечание версии hello поддерживается для подключаемого модуля является точка пересечения упоминаются в под разделом.</span><span class="sxs-lookup"><span data-stu-id="bacfc-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="bacfc-116">Сервер является точка пересечения доступен в Интернете особенно tooAzure входа AD для проверки подлинности и необходимо будет tooreceive hello токена из Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="bacfc-117">в Confluence должны быть настроены учетные данные администратора;</span><span class="sxs-lookup"><span data-stu-id="bacfc-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="bacfc-118">в Confluence должна быть отключена поддержка WebSudo;</span><span class="sxs-lookup"><span data-stu-id="bacfc-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="bacfc-119">Тестовый пользователь, созданные в hello является точка пересечения серверного приложения</span><span class="sxs-lookup"><span data-stu-id="bacfc-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="bacfc-120">в этом учебнике шаги tootest hello, не рекомендуется использовать рабочей среде является точка пересечения.</span><span class="sxs-lookup"><span data-stu-id="bacfc-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="bacfc-121">Сначала протестируйте интеграцию hello в разработки или промежуточной среде приложения hello, а затем используйте hello рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bacfc-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="bacfc-122">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bacfc-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bacfc-123">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bacfc-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bacfc-124">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bacfc-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="bacfc-125">Поддерживаемые версии Confluence</span><span class="sxs-lookup"><span data-stu-id="bacfc-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="bacfc-126">Сейчас поддерживаются следующие версии Confluence:</span><span class="sxs-lookup"><span data-stu-id="bacfc-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="bacfc-127">Является точка пересечения: 5.0 too5.10</span><span class="sxs-lookup"><span data-stu-id="bacfc-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bacfc-128">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bacfc-128">Scenario description</span></span>
<span data-ttu-id="bacfc-129">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bacfc-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bacfc-130">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bacfc-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bacfc-131">Добавление единого входа SAML является точка пересечения корпорацией Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bacfc-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="bacfc-132">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="bacfc-133">Добавление единого входа SAML является точка пересечения корпорацией Майкрософт из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bacfc-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="bacfc-134">tooconfigure hello интеграции единого входа SAML является точка пересечения корпорацией Майкрософт в Azure AD, вы должны tooadd единого входа SAML является точка пересечения корпорацией Майкрософт из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bacfc-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bacfc-135">**tooadd единого входа SAML является точка пересечения корпорацией Майкрософт из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bacfc-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacfc-136">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bacfc-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bacfc-138">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bacfc-139">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-139">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bacfc-141">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bacfc-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bacfc-143">Введите в поле поиска hello **единого входа SAML является точка пересечения корпорацией Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="bacfc-145">В панели результатов hello выберите **единого входа SAML является точка пересечения корпорацией Майкрософт**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bacfc-147">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bacfc-148">В этом разделе описывается настройка и проверка единого входа Azure AD в Confluence SAML SSO by Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bacfc-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bacfc-149">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в единый вход SAML является точка пересечения корпорацией Майкрософт является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bacfc-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="bacfc-150">Другими словами связи между пользователя Azure AD и связанных пользователей hello в единый вход SAML является точка пересечения корпорацией Майкрософт должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bacfc-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="bacfc-151">В единый вход SAML является точка пересечения корпорацией Майкрософт, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="bacfc-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bacfc-152">tooconfigure и тестирования Azure AD единого входа с помощью единого входа SAML является точка пересечения корпорацией Майкрософт, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bacfc-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bacfc-153">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bacfc-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bacfc-154">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bacfc-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bacfc-155">**[Создание единого входа SAML является точка пересечения теста пользователем Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave аналог Саймон Britta в единый вход SAML является точка пересечения корпорацией Майкрософт, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bacfc-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bacfc-156">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bacfc-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bacfc-157">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bacfc-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bacfc-158">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bacfc-159">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш единого входа SAML является точка пересечения приложением Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bacfc-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="bacfc-160">**tooconfigure Azure AD единого входа с помощью единого входа SAML является точка пересечения корпорацией Майкрософт, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bacfc-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacfc-161">В hello в hello портала Azure **единого входа SAML является точка пересечения корпорацией Майкрософт** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bacfc-163">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bacfc-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="bacfc-165">На hello **единого входа SAML является точка пересечения с URL-адреса и домена Microsoft** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bacfc-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="bacfc-167">а.</span><span class="sxs-lookup"><span data-stu-id="bacfc-167">a.</span></span> <span data-ttu-id="bacfc-168">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="bacfc-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="bacfc-169">b.</span><span class="sxs-lookup"><span data-stu-id="bacfc-169">b.</span></span> <span data-ttu-id="bacfc-170">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="bacfc-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="bacfc-171">c.</span><span class="sxs-lookup"><span data-stu-id="bacfc-171">c.</span></span> <span data-ttu-id="bacfc-172">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="bacfc-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bacfc-173">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="bacfc-173">These values are not real.</span></span> <span data-ttu-id="bacfc-174">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="bacfc-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bacfc-175">Если это именованный URL-адрес, то порт указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="bacfc-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="bacfc-176">Эти значения будут получены во время настройки hello является точка пересечения подключаемого модуля, который описывается далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="bacfc-177">toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bacfc-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="bacfc-178">а.</span><span class="sxs-lookup"><span data-stu-id="bacfc-178">a.</span></span> <span data-ttu-id="bacfc-179">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-179">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="bacfc-181">b.</span><span class="sxs-lookup"><span data-stu-id="bacfc-181">b.</span></span> <span data-ttu-id="bacfc-182">Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="bacfc-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="bacfc-184">c.</span><span class="sxs-lookup"><span data-stu-id="bacfc-184">c.</span></span> <span data-ttu-id="bacfc-185">Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="bacfc-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="bacfc-187">d.</span><span class="sxs-lookup"><span data-stu-id="bacfc-187">d.</span></span> <span data-ttu-id="bacfc-188">Теперь перейдите на странице свойств toohello **единого входа SAML является точка пересечения корпорацией Майкрософт** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="bacfc-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="bacfc-190">д.</span><span class="sxs-lookup"><span data-stu-id="bacfc-190">e.</span></span> <span data-ttu-id="bacfc-191">Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` и скопируйте это значение в блокноте, как используется позднее для конфигурации hello hello подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="bacfc-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="bacfc-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bacfc-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bacfc-194">Обратитесь к [Microsoft](mailto:waadpartners@microsoft.com) с hello следующую информацию для подключаемого модуля является точка пересечения hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="bacfc-195">Имя клиента:</span><span class="sxs-lookup"><span data-stu-id="bacfc-195">Customer Name:</span></span>
    *   <span data-ttu-id="bacfc-196">Основное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="bacfc-196">Primary domain name:</span></span>
    *   <span data-ttu-id="bacfc-197">Azure AD Premium: Да/Нет (подключаемого модуля будут доступны tooall hello клиента Free, Basic и Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="bacfc-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="bacfc-198">Число пользователей, которые будут использовать данную интеграцию:</span><span class="sxs-lookup"><span data-stu-id="bacfc-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="bacfc-199">Версия Confluence:</span><span class="sxs-lookup"><span data-stu-id="bacfc-199">Confluence Version:</span></span>
    *   <span data-ttu-id="bacfc-200">Комментарии.</span><span class="sxs-lookup"><span data-stu-id="bacfc-200">Comments:</span></span>

7. <span data-ttu-id="bacfc-201">В другом окне браузера войдите в экземпляр является точка пересечения tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="bacfc-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="bacfc-202">Наведите указатель мыши на шестеренки и выберите hello **надстройки**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="bacfc-204">На вкладке "Надстройки" щелкните **Управление надстройками**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="bacfc-206">Вручную Загрузите подключаемый модуль hello, предоставляемых корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bacfc-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="bacfc-207">Если установлен подключаемый модуль hello, оно появляется в **пользователь установил** надстройки раздел **Управление надстройками** раздела.</span><span class="sxs-lookup"><span data-stu-id="bacfc-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="bacfc-208">Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="bacfc-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="bacfc-209">Выполните следующие действия на странице настройки:</span><span class="sxs-lookup"><span data-stu-id="bacfc-209">Perform following steps on configuration page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="bacfc-211">а.</span><span class="sxs-lookup"><span data-stu-id="bacfc-211">a.</span></span> <span data-ttu-id="bacfc-212">В **URL-адрес метаданных** вставьте hello **URL-адрес метаданных** создаются из Azure AD и щелкните hello **Разрешить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="bacfc-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="bacfc-213">Считывает URL-адрес метаданных поставщика удостоверений hello и заполняет все сведения о полях hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="bacfc-214">По умолчанию идентификатор пользователя SAML указан в идентификаторе имени.</span><span class="sxs-lookup"><span data-stu-id="bacfc-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="bacfc-215">Можно изменить этот параметр tooan атрибута и введите имя соответствующего атрибута hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="bacfc-216">Убедитесь, что имеется только один сертификат, сопоставленных с приложение hello, таким образом, не содержит ошибок в разрешении метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="bacfc-217">Если имеется несколько сертификатов, при разрешении метаданных hello admin возвращает ошибку.</span><span class="sxs-lookup"><span data-stu-id="bacfc-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="bacfc-218">b.</span><span class="sxs-lookup"><span data-stu-id="bacfc-218">b.</span></span> <span data-ttu-id="bacfc-219">Копировать hello **идентификатор, URL-адрес ответа и URL-адрес входа** значения и вставьте их в **идентификатор, URL-адрес ответа и URL-адрес входа** соответственно, в текстовых полях **единого входа SAML является точка пересечения с URL-адреса и домена Microsoft**  раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bacfc-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="bacfc-220">c.</span><span class="sxs-lookup"><span data-stu-id="bacfc-220">c.</span></span> <span data-ttu-id="bacfc-221">В **имя кнопки входа** имя типа hello кнопки организация хочет hello toosee пользователей на экране входа.</span><span class="sxs-lookup"><span data-stu-id="bacfc-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="bacfc-222">d.</span><span class="sxs-lookup"><span data-stu-id="bacfc-222">d.</span></span> <span data-ttu-id="bacfc-223">В **размещение идентификатора пользователя SAML** выберите либо **идентификатор пользователя находится в элементе NameIdentifier hello hello оператора Subject** или **идентификатор пользователя — это элемент атрибута**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="bacfc-224">Этот идентификатор имеет идентификатор пользователя является точка пересечения toobe hello. Если идентификатор пользователя hello нет соответствия, система не позволит пользователям toolog в.</span><span class="sxs-lookup"><span data-stu-id="bacfc-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="bacfc-225">д.</span><span class="sxs-lookup"><span data-stu-id="bacfc-225">e.</span></span> <span data-ttu-id="bacfc-226">При выборе **идентификатор пользователя — это элемент атрибута** параметр, а затем в **имя атрибута** текстовое поле типа hello имя атрибута hello, где ожидается идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="bacfc-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="bacfc-227">f.</span><span class="sxs-lookup"><span data-stu-id="bacfc-227">f.</span></span> <span data-ttu-id="bacfc-228">При использовании hello федеративного домена (например, служб федерации Active Directory и т.д.) в Azure AD выберите команду hello **включения обнаружения домашней области** и настройте hello **доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="bacfc-229">ж.</span><span class="sxs-lookup"><span data-stu-id="bacfc-229">g.</span></span> <span data-ttu-id="bacfc-230">В **доменное имя** типа hello доменное имя здесь в случае входа на основе ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="bacfc-231">h.</span><span class="sxs-lookup"><span data-stu-id="bacfc-231">h.</span></span> <span data-ttu-id="bacfc-232">Проверьте **Включить единый Выход** при необходимости toolog out из Azure AD, когда пользователь выполняет выход из является точка пересечения.</span><span class="sxs-lookup"><span data-stu-id="bacfc-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="bacfc-233">i.</span><span class="sxs-lookup"><span data-stu-id="bacfc-233">i.</span></span> <span data-ttu-id="bacfc-234">Нажмите кнопку **Сохранить** кнопку Параметры toosave hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="bacfc-235">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bacfc-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bacfc-236">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bacfc-237">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bacfc-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bacfc-238">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bacfc-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="bacfc-239">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bacfc-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bacfc-241">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bacfc-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacfc-242">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bacfc-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bacfc-244">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bacfc-246">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bacfc-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bacfc-248">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bacfc-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bacfc-250">а.</span><span class="sxs-lookup"><span data-stu-id="bacfc-250">a.</span></span> <span data-ttu-id="bacfc-251">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bacfc-252">b.</span><span class="sxs-lookup"><span data-stu-id="bacfc-252">b.</span></span> <span data-ttu-id="bacfc-253">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bacfc-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bacfc-254">c.</span><span class="sxs-lookup"><span data-stu-id="bacfc-254">c.</span></span> <span data-ttu-id="bacfc-255">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bacfc-256">d.</span><span class="sxs-lookup"><span data-stu-id="bacfc-256">d.</span></span> <span data-ttu-id="bacfc-257">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="bacfc-258">Создание тестового пользователя Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="bacfc-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="bacfc-259">Пользователи toolog tooenable Azure AD в tooConfluence на локальном сервере, их необходимо подготовить в единый вход SAML является точка пересечения корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bacfc-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="bacfc-260">Для Confluence SAML SSO by Microsoft подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="bacfc-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="bacfc-261">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bacfc-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacfc-262">Войдите в tooyour является точка пересечения на локальном сервере от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="bacfc-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="bacfc-263">Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-263">Hover on cog and click hello **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="bacfc-265">В разделе "Users" (Пользователи) выберите вкладку **Add users** (Добавление пользователей). На hello **«Добавить пользователя»** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bacfc-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="bacfc-267">а.</span><span class="sxs-lookup"><span data-stu-id="bacfc-267">a.</span></span> <span data-ttu-id="bacfc-268">В hello **Username** текстовое поле, адреса электронной почты пользователя, например Саймон Britta для hello типа.</span><span class="sxs-lookup"><span data-stu-id="bacfc-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="bacfc-269">b.</span><span class="sxs-lookup"><span data-stu-id="bacfc-269">b.</span></span> <span data-ttu-id="bacfc-270">В hello **полное имя** текстового поля, типа hello полное имя пользователя как Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bacfc-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="bacfc-271">c.</span><span class="sxs-lookup"><span data-stu-id="bacfc-271">c.</span></span> <span data-ttu-id="bacfc-272">В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bacfc-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="bacfc-273">d.</span><span class="sxs-lookup"><span data-stu-id="bacfc-273">d.</span></span> <span data-ttu-id="bacfc-274">В hello **пароль** текстового поля, типа hello пароль для Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bacfc-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="bacfc-275">д.</span><span class="sxs-lookup"><span data-stu-id="bacfc-275">e.</span></span> <span data-ttu-id="bacfc-276">Нажмите кнопку **подтверждение пароля** вводить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="bacfc-277">f.</span><span class="sxs-lookup"><span data-stu-id="bacfc-277">f.</span></span> <span data-ttu-id="bacfc-278">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bacfc-279">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bacfc-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bacfc-280">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooConfluence единого входа SAML корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bacfc-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bacfc-282">**tooassign tooConfluence Britta Simon единого входа SAML корпорацией Майкрософт, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bacfc-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="bacfc-283">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bacfc-285">В списке приложений hello выберите **единого входа SAML является точка пересечения корпорацией Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="bacfc-287">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bacfc-289">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-289">Click **Add** button.</span></span> <span data-ttu-id="bacfc-290">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bacfc-292">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bacfc-293">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bacfc-294">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bacfc-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bacfc-295">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bacfc-295">Testing single sign-on</span></span>

<span data-ttu-id="bacfc-296">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bacfc-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bacfc-297">При нажатии кнопки hello единого входа SAML является точка пересечения с Microsoft плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour единого входа SAML является точка пересечения приложением Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bacfc-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="bacfc-298">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bacfc-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bacfc-299">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bacfc-299">Additional resources</span></span>

* [<span data-ttu-id="bacfc-300">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bacfc-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bacfc-301">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bacfc-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

