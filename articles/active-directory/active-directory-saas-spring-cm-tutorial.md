---
title: "Руководство по интеграции Azure Active Directory с SpringCM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="81d7e-103">Руководство. Интеграция Azure Active Directory с SpringCM</span><span class="sxs-lookup"><span data-stu-id="81d7e-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="81d7e-104">В этом учебнике вы узнаете, как toointegrate SpringCM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81d7e-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81d7e-105">Интеграция SpringCM с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="81d7e-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81d7e-106">Можно управлять в Azure AD, имеющего доступ tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="81d7e-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="81d7e-107">Можно включить на пользователей tooautomatically get вошедшего tooSpringCM (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="81d7e-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81d7e-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="81d7e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81d7e-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81d7e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81d7e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="81d7e-110">Prerequisites</span></span>

<span data-ttu-id="81d7e-111">tooconfigure интеграция Azure AD с SpringCM требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="81d7e-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="81d7e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="81d7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81d7e-113">подписка SpringCM с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="81d7e-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81d7e-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="81d7e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81d7e-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="81d7e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81d7e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="81d7e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81d7e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81d7e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81d7e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="81d7e-118">Scenario description</span></span>
<span data-ttu-id="81d7e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="81d7e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81d7e-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="81d7e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81d7e-121">Добавление SpringCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="81d7e-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="81d7e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="81d7e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="81d7e-123">Добавление SpringCM из галереи hello</span><span class="sxs-lookup"><span data-stu-id="81d7e-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="81d7e-124">tooconfigure hello интеграции SpringCM в Azure AD, вы должны tooadd SpringCM из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="81d7e-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81d7e-125">**tooadd SpringCM из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d7e-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="81d7e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81d7e-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81d7e-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="81d7e-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="81d7e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="81d7e-133">Введите в поле поиска hello **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-133">In hello search box, type **SpringCM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="81d7e-135">В панели результатов hello выберите **SpringCM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81d7e-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81d7e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="81d7e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81d7e-138">В этом разделе описана настройка и проверка единого входа Azure AD в SpringCM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81d7e-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81d7e-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SpringCM является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81d7e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="81d7e-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в SpringCM должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="81d7e-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="81d7e-141">В SpringCM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="81d7e-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81d7e-142">tooconfigure и теста Azure AD единого входа с SpringCM, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="81d7e-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81d7e-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="81d7e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81d7e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="81d7e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81d7e-145">**[Создание тестового пользователя SpringCM](#creating-a-springcm-test-user)**  -toohave аналог Саймон Britta в SpringCM, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="81d7e-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81d7e-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="81d7e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81d7e-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="81d7e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81d7e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="81d7e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81d7e-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение SpringCM.</span><span class="sxs-lookup"><span data-stu-id="81d7e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="81d7e-150">**tooconfigure Azure AD единого входа с SpringCM, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d7e-151">В hello в hello портала Azure **SpringCM** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="81d7e-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="81d7e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="81d7e-155">На hello **URL-адреса и домена SpringCM** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="81d7e-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="81d7e-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="81d7e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81d7e-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="81d7e-158">This value is not real.</span></span> <span data-ttu-id="81d7e-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="81d7e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="81d7e-160">Обратитесь к [группа поддержки клиента SpringCM](https://knowledge.springcm.com/support) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="81d7e-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="81d7e-161">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="81d7e-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="81d7e-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="81d7e-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81d7e-165">На hello **конфигурации SpringCM** щелкните **Настройка SpringCM** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="81d7e-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="81d7e-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="81d7e-168">В другом окне браузера, войдите на tooyour **SpringCM** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="81d7e-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="81d7e-169">В меню hello hello верхней части страницы, нажмите кнопку **перейти к**, нажмите кнопку **предпочтения**, а затем в hello **предпочтения учетной записи** щелкните **единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="81d7e-170">![Единый вход SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="81d7e-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="81d7e-171">В hello разделе Конфигурация поставщика удостоверений выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="81d7e-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="81d7e-172">![Конфигурация поставщика удостоверений](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Конфигурация поставщика удостоверений")</span><span class="sxs-lookup"><span data-stu-id="81d7e-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="81d7e-173">а.</span><span class="sxs-lookup"><span data-stu-id="81d7e-173">a.</span></span> <span data-ttu-id="81d7e-174">tooupload Скачанный сертификат Azure Active Directory, нажмите кнопку **выбрать сертификат издателя** или **изменить сертификат издателя**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="81d7e-175">b.</span><span class="sxs-lookup"><span data-stu-id="81d7e-175">b.</span></span> <span data-ttu-id="81d7e-176">Вставить **идентификатор сущности SAML** значение, которое было скопировано из портала Azure в hello **издателя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="81d7e-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="81d7e-177">c.</span><span class="sxs-lookup"><span data-stu-id="81d7e-177">c.</span></span> <span data-ttu-id="81d7e-178">Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **инициированная конечная точка Service Provider (SP)** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="81d7e-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="81d7e-179">d.</span><span class="sxs-lookup"><span data-stu-id="81d7e-179">d.</span></span> <span data-ttu-id="81d7e-180">Для параметра **SAML Enabled** (SAML включен) установите значение **Enabled** (Включено).</span><span class="sxs-lookup"><span data-stu-id="81d7e-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="81d7e-181">д.</span><span class="sxs-lookup"><span data-stu-id="81d7e-181">e.</span></span> <span data-ttu-id="81d7e-182">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="81d7e-183">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="81d7e-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81d7e-184">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="81d7e-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81d7e-185">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81d7e-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81d7e-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="81d7e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="81d7e-187">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="81d7e-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="81d7e-189">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d7e-190">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="81d7e-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81d7e-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81d7e-194">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="81d7e-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81d7e-196">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="81d7e-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81d7e-198">а.</span><span class="sxs-lookup"><span data-stu-id="81d7e-198">a.</span></span> <span data-ttu-id="81d7e-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81d7e-200">b.</span><span class="sxs-lookup"><span data-stu-id="81d7e-200">b.</span></span> <span data-ttu-id="81d7e-201">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81d7e-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81d7e-202">c.</span><span class="sxs-lookup"><span data-stu-id="81d7e-202">c.</span></span> <span data-ttu-id="81d7e-203">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81d7e-204">d.</span><span class="sxs-lookup"><span data-stu-id="81d7e-204">d.</span></span> <span data-ttu-id="81d7e-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="81d7e-206">Создание тестового пользователя SpringCM</span><span class="sxs-lookup"><span data-stu-id="81d7e-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="81d7e-207">toolog пользователей Azure Active Directory tooenable в tooSpringCM, их необходимо подготовить в SpringCM.</span><span class="sxs-lookup"><span data-stu-id="81d7e-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="81d7e-208">В случае hello объекта SpringCM Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="81d7e-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="81d7e-209">Дополнительные сведения см. в статье [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (Создание и изменение пользователя SpringCM).</span><span class="sxs-lookup"><span data-stu-id="81d7e-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="81d7e-210">**tooprovision tooSpringCM учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d7e-211">Войдите в tooyour **SpringCM** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="81d7e-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="81d7e-212">Щелкните **GO TO** (Перейти), а затем — **ADDRESS BOOK** (Адресная книга).</span><span class="sxs-lookup"><span data-stu-id="81d7e-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="81d7e-213">![Создание пользователя](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="81d7e-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="81d7e-214">Щелкните **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-214">Click **Create User**.</span></span>

4. <span data-ttu-id="81d7e-215">Выберите **роль пользователя**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="81d7e-216">Установите флажок **Отправить сообщение для активации**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="81d7e-217">Тип hello имя, фамилию и адрес электронной почты действующей учетной записи Azure Active Directory, требуется tooprovision в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="81d7e-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="81d7e-218">Добавить пользователя tooa hello **группы безопасности**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="81d7e-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="81d7e-220">Можно использовать любые другие SpringCM пользователя средства создания учетных записей или интерфейсы API, предоставляемые SpringCM tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="81d7e-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81d7e-221">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="81d7e-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81d7e-222">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSpringCM доступа.</span><span class="sxs-lookup"><span data-stu-id="81d7e-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="81d7e-224">**tooassign tooSpringCM Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="81d7e-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d7e-225">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="81d7e-227">В списке приложений hello выберите **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-227">In hello applications list, select **SpringCM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="81d7e-229">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="81d7e-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-231">Click **Add** button.</span></span> <span data-ttu-id="81d7e-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="81d7e-234">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="81d7e-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81d7e-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81d7e-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="81d7e-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81d7e-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="81d7e-237">Testing single sign-on</span></span>

<span data-ttu-id="81d7e-238">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="81d7e-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="81d7e-239">При нажатии кнопки hello SpringCM плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на SpringCM приложения.</span><span class="sxs-lookup"><span data-stu-id="81d7e-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="81d7e-240">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81d7e-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="81d7e-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="81d7e-241">Additional resources</span></span>

* [<span data-ttu-id="81d7e-242">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81d7e-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81d7e-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81d7e-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

