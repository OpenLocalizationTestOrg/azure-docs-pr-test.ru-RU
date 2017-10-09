---
title: "Руководство. Интеграция Azure Active Directory с GitHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="d8714-103">Руководство. Интеграция Azure Active Directory с GitHub</span><span class="sxs-lookup"><span data-stu-id="d8714-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="d8714-104">В этом учебнике вы узнаете, как toointegrate GitHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8714-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8714-105">Интеграция GitHub с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d8714-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8714-106">Можно управлять в Azure AD, имеющего доступ tooGitHub</span><span class="sxs-lookup"><span data-stu-id="d8714-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="d8714-107">Можно включить на пользователей tooautomatically get вошедшего tooGitHub (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8714-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="d8714-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d8714-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8714-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8714-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d8714-110">Prerequisites</span></span>

<span data-ttu-id="d8714-111">tooconfigure интеграция Azure AD с GitHub требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d8714-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="d8714-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d8714-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8714-113">подписка GitHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d8714-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d8714-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d8714-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d8714-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d8714-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8714-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="d8714-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d8714-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8714-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d8714-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d8714-118">Scenario description</span></span>
<span data-ttu-id="d8714-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d8714-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8714-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d8714-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8714-121">Добавление GitHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d8714-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="d8714-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="d8714-123">Добавление GitHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d8714-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="d8714-124">tooconfigure hello интеграции GitHub в Azure AD, вы должны tooadd GitHub из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d8714-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8714-125">**tooadd GitHub из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d8714-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8714-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d8714-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8714-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d8714-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8714-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d8714-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d8714-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d8714-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d8714-133">Введите в поле поиска hello **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="d8714-133">In hello search box, type **GitHub.com**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="d8714-135">В панели результатов hello выберите **GitHub**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d8714-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8714-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8714-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в GitHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8714-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8714-139">Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в GitHub — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8714-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="d8714-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в GitHub должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d8714-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="d8714-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8714-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="d8714-142">tooconfigure и теста Azure AD единого входа с GitHub, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d8714-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8714-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d8714-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8714-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d8714-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8714-145">**[Создание тестового пользователя GitHub](#creating-a-GitHub-test-user)**  -toohave аналог Саймон Britta в GitHub, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="d8714-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d8714-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d8714-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8714-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d8714-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8714-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8714-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложение GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8714-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="d8714-150">**tooconfigure Azure AD единого входа с GitHub, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d8714-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8714-151">На портале управления Azure hello на hello **GitHub** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d8714-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d8714-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d8714-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="d8714-155">На hello **URL-адреса и домена GitHub** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d8714-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="d8714-157">а.</span><span class="sxs-lookup"><span data-stu-id="d8714-157">a.</span></span> <span data-ttu-id="d8714-158">В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="d8714-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="d8714-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8714-159">b.</span></span> <span data-ttu-id="d8714-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="d8714-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8714-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="d8714-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d8714-162">У вас tooupdate эти значения с hello фактический ющего на URL-адрес и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d8714-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="d8714-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d8714-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d8714-164">Перейдите в раздел tooretrieve tooGitHub Admin эти значения.</span><span class="sxs-lookup"><span data-stu-id="d8714-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="d8714-165">На hello **атрибуты пользователя** выберите **идентификатор пользователя** как user.mail.</span><span class="sxs-lookup"><span data-stu-id="d8714-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="d8714-167">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="d8714-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="d8714-169">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="d8714-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="d8714-170">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d8714-170">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="d8714-172">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d8714-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="d8714-174">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8714-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="d8714-176">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d8714-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="d8714-178">На hello **конфигурации GitHub** щелкните **настройки GitHub** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="d8714-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="d8714-181">В другом окне веб-браузера войдите на свой корпоративный сайт GitHub в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d8714-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="d8714-182">Перейдите в слишком**параметры** и нажмите кнопку **безопасности**</span><span class="sxs-lookup"><span data-stu-id="d8714-182">Navigate too**Settings** and click **Security**</span></span>

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="d8714-184">Проверьте hello **включить проверку подлинности SAML** поле, отображая hello единым входом поля конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d8714-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="d8714-185">Затем с помощью hello единого входа URL-адреса значение tooupdate hello один URL-адрес входа в конфигурации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8714-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="d8714-187">Настройте hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="d8714-187">Configure hello following fields:</span></span>

    <span data-ttu-id="d8714-188">а.</span><span class="sxs-lookup"><span data-stu-id="d8714-188">a.</span></span> <span data-ttu-id="d8714-189">**URL-адрес входа**: введите **SAML единого входа для URL-адрес службы** из hello **настройки GitHub** раздел в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d8714-190">b.</span><span class="sxs-lookup"><span data-stu-id="d8714-190">b.</span></span> <span data-ttu-id="d8714-191">**Издатель**: введите **идентификатор сущности SAML** из hello **настройки GitHub** раздел в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d8714-192">c.</span><span class="sxs-lookup"><span data-stu-id="d8714-192">c.</span></span> <span data-ttu-id="d8714-193">**Открытый сертификат**: Привет открыть загрузить сертификат из Azure AD в Блокноте и скопируйте содержимое hello, включая «BEGIN» и «END сертификата»</span><span class="sxs-lookup"><span data-stu-id="d8714-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="d8714-195">Щелкните **конфигурация теста SAML** tooconfirm, без проверки ошибок или ошибок во время единого входа.</span><span class="sxs-lookup"><span data-stu-id="d8714-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="d8714-197">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="d8714-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8714-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8714-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8714-199">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d8714-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d8714-201">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d8714-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8714-202">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d8714-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8714-204">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="d8714-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8714-206">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d8714-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8714-208">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d8714-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8714-210">а.</span><span class="sxs-lookup"><span data-stu-id="d8714-210">a.</span></span> <span data-ttu-id="d8714-211">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8714-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8714-212">b.</span><span class="sxs-lookup"><span data-stu-id="d8714-212">b.</span></span> <span data-ttu-id="d8714-213">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8714-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8714-214">c.</span><span class="sxs-lookup"><span data-stu-id="d8714-214">c.</span></span> <span data-ttu-id="d8714-215">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d8714-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8714-216">d.</span><span class="sxs-lookup"><span data-stu-id="d8714-216">d.</span></span> <span data-ttu-id="d8714-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d8714-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="d8714-218">Создание тестового пользователя GitHub</span><span class="sxs-lookup"><span data-stu-id="d8714-218">Creating a GitHub test user</span></span>

<span data-ttu-id="d8714-219">В порядке tooenable toolog пользователей Azure AD в GitHub их необходимо подготовить в GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8714-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="d8714-220">В случае hello GitHub Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="d8714-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="d8714-221">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="d8714-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8714-222">Войдите в систему tooyour GitHub сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="d8714-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="d8714-223">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d8714-223">Click **People**.</span></span>

    <span data-ttu-id="d8714-224">![Люди](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="d8714-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="d8714-225">Нажмите **Invite member** (Пригласить участника).</span><span class="sxs-lookup"><span data-stu-id="d8714-225">Click **Invite member**.</span></span>

    <span data-ttu-id="d8714-226">![Приглашение пользователей](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="d8714-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="d8714-227">На hello **приглашение элемент** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d8714-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="d8714-228">а.</span><span class="sxs-lookup"><span data-stu-id="d8714-228">a.</span></span> <span data-ttu-id="d8714-229">В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d8714-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="d8714-230">![Приглашение участников](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="d8714-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="d8714-231">b.</span><span class="sxs-lookup"><span data-stu-id="d8714-231">b.</span></span> <span data-ttu-id="d8714-232">Щелкните **Send Invitation** (Отправить приглашение).</span><span class="sxs-lookup"><span data-stu-id="d8714-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="d8714-233">![Приглашение участников](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="d8714-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8714-234">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="d8714-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8714-235">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d8714-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8714-236">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooGitHub доступа.</span><span class="sxs-lookup"><span data-stu-id="d8714-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d8714-238">**tooassign tooGitHub Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d8714-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8714-239">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d8714-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d8714-241">В списке приложений hello выберите **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="d8714-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="d8714-243">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d8714-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d8714-245">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d8714-245">Click **Add** button.</span></span> <span data-ttu-id="d8714-246">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d8714-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d8714-248">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d8714-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8714-249">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d8714-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8714-250">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d8714-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d8714-251">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d8714-251">Testing single sign-on</span></span>

<span data-ttu-id="d8714-252">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d8714-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8714-253">При нажатии кнопки hello GitHub плитки в панели доступа hello, вы должны получить вошедшего tooyour GitHub приложения.</span><span class="sxs-lookup"><span data-stu-id="d8714-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="d8714-254">Вы сможете вход как учетная запись организации, но затем toolog необходимость личную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d8714-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d8714-255">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d8714-255">Additional resources</span></span>

* [<span data-ttu-id="d8714-256">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8714-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8714-257">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8714-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
