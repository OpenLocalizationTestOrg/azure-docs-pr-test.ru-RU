---
title: "Руководство по интеграции Azure Active Directory с Pantheon | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="35c3b-103">Руководство по интеграции Azure Active Directory с Pantheon</span><span class="sxs-lookup"><span data-stu-id="35c3b-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="35c3b-104">В этом учебнике вы узнаете, как toointegrate Pantheon с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35c3b-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35c3b-105">Интеграция с Azure AD Pantheon предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="35c3b-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35c3b-106">Можно управлять в Azure AD, имеющего доступ tooPantheon</span><span class="sxs-lookup"><span data-stu-id="35c3b-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="35c3b-107">Можно включить на пользователей tooautomatically get вошедшего tooPantheon (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="35c3b-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35c3b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="35c3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35c3b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35c3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35c3b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="35c3b-110">Prerequisites</span></span>

<span data-ttu-id="35c3b-111">tooconfigure интеграция Azure AD с Pantheon требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="35c3b-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="35c3b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="35c3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35c3b-113">подписка Pantheon с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="35c3b-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35c3b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="35c3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35c3b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="35c3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35c3b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="35c3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35c3b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35c3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35c3b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="35c3b-118">Scenario description</span></span>
<span data-ttu-id="35c3b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="35c3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35c3b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="35c3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35c3b-121">Добавление Pantheon из галереи hello</span><span class="sxs-lookup"><span data-stu-id="35c3b-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="35c3b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="35c3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="35c3b-123">Добавление Pantheon из галереи hello</span><span class="sxs-lookup"><span data-stu-id="35c3b-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="35c3b-124">tooconfigure hello интеграции Pantheon в Azure AD, вы должны tooadd Pantheon из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="35c3b-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35c3b-125">**tooadd Pantheon из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="35c3b-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35c3b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="35c3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35c3b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35c3b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="35c3b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="35c3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="35c3b-133">Введите в поле поиска hello **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-133">In hello search box, type **Pantheon**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="35c3b-135">В панели результатов hello выберите **Pantheon**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35c3b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="35c3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35c3b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Pantheon с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35c3b-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35c3b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Pantheon является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35c3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="35c3b-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Pantheon должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="35c3b-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="35c3b-141">В Pantheon, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="35c3b-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35c3b-142">tooconfigure и теста Azure AD единого входа с Pantheon, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="35c3b-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35c3b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="35c3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35c3b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="35c3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35c3b-145">**[Создание тестового пользователя Pantheon](#creating-a-pantheon-test-user)**  -toohave аналог Саймон Britta в Pantheon, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="35c3b-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35c3b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="35c3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35c3b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="35c3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35c3b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="35c3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35c3b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Pantheon.</span><span class="sxs-lookup"><span data-stu-id="35c3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="35c3b-150">**tooconfigure Azure AD единого входа с Pantheon, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="35c3b-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="35c3b-151">В hello в hello портала Azure **Pantheon** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="35c3b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="35c3b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="35c3b-155">На hello **URL-адреса и домена Pantheon** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="35c3b-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="35c3b-157">а.</span><span class="sxs-lookup"><span data-stu-id="35c3b-157">a.</span></span> <span data-ttu-id="35c3b-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="35c3b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="35c3b-159">b.</span><span class="sxs-lookup"><span data-stu-id="35c3b-159">b.</span></span> <span data-ttu-id="35c3b-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="35c3b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35c3b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="35c3b-161">These values are not real.</span></span> <span data-ttu-id="35c3b-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="35c3b-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="35c3b-163">Обратитесь к [Pantheon поддержки](https://pantheon.io/docs/getting-support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="35c3b-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="35c3b-164">Pantheon приложение ожидает утверждения SAML hello в определенном формате, поэтому требуется вы tooset hello значения атрибута идентификатор пользователя с помощью адреса электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="35c3b-165">По умолчанию Azure AD использует hello UserPrincipalName атрибута идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="35c3b-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="35c3b-166">Однако для успешной интеграции требуют tooadjust toomatch это значение с адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="35c3b-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="35c3b-167">Интеграция Hello будет работать только после выполнения hello правильное сопоставление.</span><span class="sxs-lookup"><span data-stu-id="35c3b-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="35c3b-169">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="35c3b-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="35c3b-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="35c3b-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="35c3b-173">На hello **конфигурации Pantheon** щелкните **Настройка Pantheon** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="35c3b-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35c3b-174">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="35c3b-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="35c3b-176">tooconfigure единого входа на **Pantheon** стороны, необходимо загрузить hello toosend **сертификат** и **SAML единого входа URL-адрес службы** слишком[Pantheon поддержки](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="35c3b-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="35c3b-177">Необходимо также tooprovide hello доменов электронной почты сведения и Дата и время при необходимости tooenable этого подключения.</span><span class="sxs-lookup"><span data-stu-id="35c3b-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="35c3b-178">Дополнительные сведения см. [здесь](https://pantheon.io/docs/sso-organizations/).</span><span class="sxs-lookup"><span data-stu-id="35c3b-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="35c3b-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="35c3b-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35c3b-180">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35c3b-181">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35c3b-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35c3b-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="35c3b-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="35c3b-183">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="35c3b-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="35c3b-185">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="35c3b-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35c3b-186">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="35c3b-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35c3b-188">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35c3b-190">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="35c3b-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35c3b-192">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="35c3b-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35c3b-194">а.</span><span class="sxs-lookup"><span data-stu-id="35c3b-194">a.</span></span> <span data-ttu-id="35c3b-195">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35c3b-196">b.</span><span class="sxs-lookup"><span data-stu-id="35c3b-196">b.</span></span> <span data-ttu-id="35c3b-197">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35c3b-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35c3b-198">c.</span><span class="sxs-lookup"><span data-stu-id="35c3b-198">c.</span></span> <span data-ttu-id="35c3b-199">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35c3b-200">d.</span><span class="sxs-lookup"><span data-stu-id="35c3b-200">d.</span></span> <span data-ttu-id="35c3b-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="35c3b-202">Создание тестового пользователя Pantheon</span><span class="sxs-lookup"><span data-stu-id="35c3b-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="35c3b-203">В этом разделе описано, как создать пользователя Britta Simon в приложении Pantheon.</span><span class="sxs-lookup"><span data-stu-id="35c3b-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="35c3b-204">Следуйте hello ниже шаги tooadd hello пользователя в Pantheon.</span><span class="sxs-lookup"><span data-stu-id="35c3b-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="35c3b-205">Для единого входа toowork пользователь должен сначала создается в Pantheon toobe.</span><span class="sxs-lookup"><span data-stu-id="35c3b-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="35c3b-206">TooPantheon входа в систему с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="35c3b-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="35c3b-207">Перейдите в слишком**организации** страницу панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="35c3b-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="35c3b-208">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-208">Click **People**.</span></span>

4. <span data-ttu-id="35c3b-209">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-209">Click **Add user**.</span></span>

5. <span data-ttu-id="35c3b-210">Введите адрес электронной почты пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="35c3b-211">Выберите роль пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="35c3b-212">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35c3b-213">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="35c3b-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35c3b-214">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPantheon доступа.</span><span class="sxs-lookup"><span data-stu-id="35c3b-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="35c3b-216">**tooassign tooPantheon Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="35c3b-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="35c3b-217">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="35c3b-219">В списке приложений hello выберите **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-219">In hello applications list, select **Pantheon**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="35c3b-221">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="35c3b-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-223">Click **Add** button.</span></span> <span data-ttu-id="35c3b-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="35c3b-226">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35c3b-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35c3b-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="35c3b-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35c3b-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="35c3b-229">Testing single sign-on</span></span>

<span data-ttu-id="35c3b-230">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="35c3b-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="35c3b-231">При нажатии кнопки hello Pantheon плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Pantheon приложения.</span><span class="sxs-lookup"><span data-stu-id="35c3b-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="35c3b-232">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35c3b-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="35c3b-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="35c3b-233">Additional resources</span></span>

* [<span data-ttu-id="35c3b-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35c3b-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35c3b-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35c3b-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

