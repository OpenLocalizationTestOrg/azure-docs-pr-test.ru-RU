---
title: "Руководство по интеграции Azure Active Directory с LockPath Keylight | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="820bb-103">Руководство по интеграции Azure Active Directory с LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="820bb-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="820bb-104">В этом учебнике вы узнаете, как toointegrate LockPath Keylight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="820bb-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="820bb-105">Интеграция с Azure AD LockPath Keylight предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="820bb-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="820bb-106">Можно управлять в Azure AD, имеющего доступ tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="820bb-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="820bb-107">Можно включить на пользователей tooautomatically get вошедшего tooLockPath Keylight (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="820bb-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="820bb-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="820bb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="820bb-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="820bb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="820bb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="820bb-110">Prerequisites</span></span>

<span data-ttu-id="820bb-111">tooconfigure интеграция Azure AD с LockPath Keylight требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="820bb-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="820bb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="820bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="820bb-113">подписка LockPath Keylight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="820bb-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="820bb-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="820bb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="820bb-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="820bb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="820bb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="820bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="820bb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="820bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="820bb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="820bb-118">Scenario description</span></span>
<span data-ttu-id="820bb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="820bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="820bb-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="820bb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="820bb-121">Добавление LockPath Keylight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="820bb-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="820bb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="820bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="820bb-123">Добавление LockPath Keylight из галереи hello</span><span class="sxs-lookup"><span data-stu-id="820bb-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="820bb-124">tooconfigure hello интеграции LockPath Keylight в Azure AD, вы должны tooadd LockPath Keylight из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="820bb-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="820bb-125">**tooadd LockPath Keylight из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="820bb-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="820bb-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="820bb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="820bb-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="820bb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="820bb-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="820bb-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="820bb-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="820bb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="820bb-133">Введите в поле поиска hello **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="820bb-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="820bb-135">В панели результатов hello выберите **LockPath Keylight**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="820bb-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="820bb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="820bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="820bb-138">В этом разделе описана настройка и проверка единого входа Azure AD в LockPath Keylight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="820bb-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="820bb-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LockPath Keylight является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="820bb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="820bb-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в LockPath Keylight должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="820bb-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="820bb-141">В LockPath Keylight, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="820bb-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="820bb-142">tooconfigure и теста Azure AD единого входа с LockPath Keylight, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="820bb-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="820bb-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="820bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="820bb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="820bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="820bb-145">**[Создание тестового пользователя LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave аналог Саймон Britta в LockPath Keylight, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="820bb-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="820bb-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="820bb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="820bb-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="820bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="820bb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="820bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="820bb-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="820bb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="820bb-150">**tooconfigure Azure AD единого входа с LockPath Keylight выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="820bb-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="820bb-151">В hello в hello портала Azure **LockPath Keylight** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="820bb-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="820bb-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="820bb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="820bb-155">На hello **URL-адреса и домена Keylight LockPath** выполните следующие шаги hello::</span><span class="sxs-lookup"><span data-stu-id="820bb-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="820bb-157">а.</span><span class="sxs-lookup"><span data-stu-id="820bb-157">a.</span></span> <span data-ttu-id="820bb-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="820bb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="820bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="820bb-159">b.</span></span> <span data-ttu-id="820bb-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="820bb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="820bb-161">c.</span><span class="sxs-lookup"><span data-stu-id="820bb-161">c.</span></span> <span data-ttu-id="820bb-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="820bb-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="820bb-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="820bb-163">These values are not real.</span></span> <span data-ttu-id="820bb-164">Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="820bb-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="820bb-165">Обратитесь к [группа поддержки клиента Keylight LockPath](https://www.lockpath.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="820bb-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="820bb-166">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="820bb-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="820bb-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="820bb-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="820bb-170">На hello **конфигурации Keylight LockPath** щелкните **Настройка LockPath Keylight** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="820bb-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="820bb-171">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="820bb-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="820bb-173">tooenable единого входа в LockPath Keylight выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="820bb-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="820bb-174">а.</span><span class="sxs-lookup"><span data-stu-id="820bb-174">a.</span></span> <span data-ttu-id="820bb-175">Вход tooyour LockPath Keylight учетной записи, от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="820bb-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="820bb-176">b.</span><span class="sxs-lookup"><span data-stu-id="820bb-176">b.</span></span> <span data-ttu-id="820bb-177">В меню в верхней части hello hello выберите **лицо**и выберите **Keylight установки**.</span><span class="sxs-lookup"><span data-stu-id="820bb-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="820bb-179">c.</span><span class="sxs-lookup"><span data-stu-id="820bb-179">c.</span></span> <span data-ttu-id="820bb-180">В treeview hello hello левой части экрана, нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="820bb-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="820bb-182">d.</span><span class="sxs-lookup"><span data-stu-id="820bb-182">d.</span></span> <span data-ttu-id="820bb-183">На hello **параметры SAML** диалоговое окно, нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="820bb-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="820bb-185">На hello **изменение параметров SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="820bb-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="820bb-187">а.</span><span class="sxs-lookup"><span data-stu-id="820bb-187">a.</span></span> <span data-ttu-id="820bb-188">Задать **проверку подлинности SAML** слишком**Active**.</span><span class="sxs-lookup"><span data-stu-id="820bb-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="820bb-189">b.</span><span class="sxs-lookup"><span data-stu-id="820bb-189">b.</span></span> <span data-ttu-id="820bb-190">Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="820bb-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="820bb-191">c.</span><span class="sxs-lookup"><span data-stu-id="820bb-191">c.</span></span> <span data-ttu-id="820bb-192">Вставить hello **URL-адрес службы единого выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="820bb-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="820bb-193">d.</span><span class="sxs-lookup"><span data-stu-id="820bb-193">d.</span></span> <span data-ttu-id="820bb-194">Нажмите кнопку **выбрать файл** tooselect вашей загруженный LockPath Keylight сертификатов и нажмите кнопку **откройте** tooupload hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="820bb-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="820bb-195">д.</span><span class="sxs-lookup"><span data-stu-id="820bb-195">e.</span></span> <span data-ttu-id="820bb-196">Задать **местоположение идентификатора пользователя SAML** слишком**элемент NameIdentifier оператора subject hello**.</span><span class="sxs-lookup"><span data-stu-id="820bb-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="820bb-197">f.</span><span class="sxs-lookup"><span data-stu-id="820bb-197">f.</span></span> <span data-ttu-id="820bb-198">Укажите hello **поставщика услуг Keylight** с помощью hello следующий шаблон: **https://&lt;CompanyName&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="820bb-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="820bb-199">ж.</span><span class="sxs-lookup"><span data-stu-id="820bb-199">g.</span></span> <span data-ttu-id="820bb-200">Задать **автоматической подготовки пользователей** слишком**Active**.</span><span class="sxs-lookup"><span data-stu-id="820bb-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="820bb-201">h.</span><span class="sxs-lookup"><span data-stu-id="820bb-201">h.</span></span> <span data-ttu-id="820bb-202">Задать **тип учетной записи Автоматическая подготовка к работе** слишком**полноправный пользователь**.</span><span class="sxs-lookup"><span data-stu-id="820bb-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="820bb-203">i.</span><span class="sxs-lookup"><span data-stu-id="820bb-203">i.</span></span> <span data-ttu-id="820bb-204">Задайте для параметра **Auto-provision security role** (Роль безопасности для автоматической подготовки) значение **Standard User with SAML** (Права обычного пользователя с SAML).</span><span class="sxs-lookup"><span data-stu-id="820bb-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="820bb-205">j.</span><span class="sxs-lookup"><span data-stu-id="820bb-205">j.</span></span> <span data-ttu-id="820bb-206">Задайте для параметра **Auto-provision security config** (Конфигурация безопасности для автоматической подготовки) значение **Standard User Configuration** (Конфигурация обычного пользователя).</span><span class="sxs-lookup"><span data-stu-id="820bb-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="820bb-207">k.</span><span class="sxs-lookup"><span data-stu-id="820bb-207">k.</span></span> <span data-ttu-id="820bb-208">В hello **атрибут адреса электронной почты** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="820bb-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="820bb-209">l.</span><span class="sxs-lookup"><span data-stu-id="820bb-209">l.</span></span> <span data-ttu-id="820bb-210">В hello **атрибут имени** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="820bb-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="820bb-211">m.</span><span class="sxs-lookup"><span data-stu-id="820bb-211">m.</span></span> <span data-ttu-id="820bb-212">В hello **атрибут фамилии** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="820bb-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="820bb-213">n.</span><span class="sxs-lookup"><span data-stu-id="820bb-213">n.</span></span> <span data-ttu-id="820bb-214">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="820bb-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="820bb-215">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="820bb-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="820bb-216">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="820bb-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="820bb-217">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="820bb-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="820bb-218">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="820bb-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="820bb-219">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="820bb-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="820bb-221">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="820bb-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="820bb-222">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="820bb-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="820bb-224">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="820bb-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="820bb-226">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="820bb-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="820bb-228">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="820bb-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="820bb-230">а.</span><span class="sxs-lookup"><span data-stu-id="820bb-230">a.</span></span> <span data-ttu-id="820bb-231">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="820bb-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="820bb-232">b.</span><span class="sxs-lookup"><span data-stu-id="820bb-232">b.</span></span> <span data-ttu-id="820bb-233">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="820bb-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="820bb-234">c.</span><span class="sxs-lookup"><span data-stu-id="820bb-234">c.</span></span> <span data-ttu-id="820bb-235">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="820bb-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="820bb-236">d.</span><span class="sxs-lookup"><span data-stu-id="820bb-236">d.</span></span> <span data-ttu-id="820bb-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="820bb-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="820bb-238">Создание тестового пользователя LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="820bb-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="820bb-239">В этом разделе описано, как создать пользователя Britta Simon в приложении LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="820bb-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="820bb-240">LockPath Keylight поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="820bb-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="820bb-241">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="820bb-241">There is no action item for you in this section.</span></span> <span data-ttu-id="820bb-242">При доступе к LockPath Keylight, если пользователь hello еще не существует, создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="820bb-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="820bb-243">Если требуется toocreate пользователя вручную, необходимо toocontact hello [LockPath Keylight клиента поддержки](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="820bb-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="820bb-244">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="820bb-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="820bb-245">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="820bb-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="820bb-247">**tooassign Britta Simon tooLockPath Keylight, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="820bb-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="820bb-248">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="820bb-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="820bb-250">В списке приложений hello выберите **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="820bb-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="820bb-252">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="820bb-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="820bb-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="820bb-254">Click **Add** button.</span></span> <span data-ttu-id="820bb-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="820bb-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="820bb-257">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="820bb-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="820bb-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="820bb-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="820bb-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="820bb-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="820bb-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="820bb-260">Testing single sign-on</span></span>

<span data-ttu-id="820bb-261">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="820bb-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="820bb-262">При нажатии кнопки LockPath Keylight плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour LockPath Keylight приложения.</span><span class="sxs-lookup"><span data-stu-id="820bb-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="820bb-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="820bb-263">Additional resources</span></span>

* [<span data-ttu-id="820bb-264">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="820bb-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="820bb-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="820bb-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

