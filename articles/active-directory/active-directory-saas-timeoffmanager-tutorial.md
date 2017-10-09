---
title: "Руководство по интеграции Azure Active Directory с TimeOffManager | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="ed22b-103">Учебник. Интеграция Azure Active Directory с TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="ed22b-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="ed22b-104">В этом учебнике вы узнаете, как toointegrate TimeOffManager с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed22b-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed22b-105">Интеграция TimeOffManager с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ed22b-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed22b-106">Можно управлять в Azure AD, имеющего доступ tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="ed22b-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="ed22b-107">Можно включить на пользователей tooautomatically get вошедшего tooTimeOffManager (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed22b-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed22b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ed22b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ed22b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed22b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed22b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed22b-110">Prerequisites</span></span>

<span data-ttu-id="ed22b-111">tooconfigure интеграция Azure AD с TimeOffManager требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ed22b-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="ed22b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ed22b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed22b-113">Подписка с поддержкой единого входа TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="ed22b-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed22b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ed22b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed22b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ed22b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed22b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ed22b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed22b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed22b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed22b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ed22b-118">Scenario description</span></span>
<span data-ttu-id="ed22b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ed22b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed22b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ed22b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed22b-121">Добавление TimeOffManager из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="ed22b-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="ed22b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed22b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="ed22b-123">Добавление TimeOffManager из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="ed22b-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="ed22b-124">tooconfigure hello интеграции TimeOffManager в Azure AD, вы должны tooadd TimeOffManager из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed22b-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed22b-125">**tooadd TimeOffManager из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed22b-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed22b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ed22b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed22b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed22b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ed22b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ed22b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ed22b-133">Введите в поле поиска hello **TimeOffManager**выберите **TimeOffManager** на панели «результат» и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ed22b-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Добавление из коллекции](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ed22b-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed22b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ed22b-136">В этом разделе описана настройка и проверка единого входа Azure AD в TimeOffManager с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed22b-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ed22b-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TimeOffManager является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed22b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="ed22b-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в TimeOffManager должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ed22b-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="ed22b-139">В TimeOffManager, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ed22b-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ed22b-140">tooconfigure и теста Azure AD единого входа с TimeOffManager, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ed22b-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed22b-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ed22b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed22b-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ed22b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed22b-143">**[Создание тестового пользователя TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave аналог Саймон Britta в TimeOffManager, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ed22b-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed22b-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ed22b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed22b-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed22b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ed22b-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed22b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ed22b-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="ed22b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="ed22b-148">**Azure AD tooconfigure единого входа с TimeOffManager, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed22b-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed22b-149">В hello в hello портала Azure **TimeOffManager** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ed22b-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed22b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Вход на основе SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="ed22b-153">На hello **URL-адреса и домена TimeOffManager** выполните hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ed22b-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Раздел "Домены и URL-адреса приложения TimeOffManager"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="ed22b-155">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="ed22b-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed22b-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ed22b-156">This value is not real.</span></span> <span data-ttu-id="ed22b-157">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="ed22b-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="ed22b-158">Можно получить это значение из **на страницу параметров единого входа** описанной далее в учебнике hello или обратитесь к [TimeOffManager поддержки](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed22b-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="ed22b-159">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed22b-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="ed22b-161">Цель этого раздела Hello — toooutline как tooTimeOffManger tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="ed22b-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="ed22b-162">Приложение TimeOffManger ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML.</span><span class="sxs-lookup"><span data-stu-id="ed22b-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="ed22b-163">пример Hello следующий снимок экрана для этого.</span><span class="sxs-lookup"><span data-stu-id="ed22b-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="ed22b-164">![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Атрибуты токена SAML")</span><span class="sxs-lookup"><span data-stu-id="ed22b-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="ed22b-165">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ed22b-165">Attribute Name</span></span> | <span data-ttu-id="ed22b-166">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ed22b-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ed22b-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="ed22b-167">Firstname</span></span> |<span data-ttu-id="ed22b-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="ed22b-168">User.givenname</span></span> |
    | <span data-ttu-id="ed22b-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="ed22b-169">Lastname</span></span> |<span data-ttu-id="ed22b-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="ed22b-170">User.surname</span></span> |
    | <span data-ttu-id="ed22b-171">Email</span><span class="sxs-lookup"><span data-stu-id="ed22b-171">Email</span></span> |<span data-ttu-id="ed22b-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="ed22b-172">User.mail</span></span> |
    
    <span data-ttu-id="ed22b-173">а.</span><span class="sxs-lookup"><span data-stu-id="ed22b-173">a.</span></span>  <span data-ttu-id="ed22b-174">Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="ed22b-175">![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Атрибуты токена SAML")</span><span class="sxs-lookup"><span data-stu-id="ed22b-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="ed22b-176">![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Атрибуты токена SAML")</span><span class="sxs-lookup"><span data-stu-id="ed22b-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="ed22b-177">b.</span><span class="sxs-lookup"><span data-stu-id="ed22b-177">b.</span></span>  <span data-ttu-id="ed22b-178">В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ed22b-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ed22b-179">c.</span><span class="sxs-lookup"><span data-stu-id="ed22b-179">c.</span></span>  <span data-ttu-id="ed22b-180">В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.</span><span class="sxs-lookup"><span data-stu-id="ed22b-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="ed22b-181">d.</span><span class="sxs-lookup"><span data-stu-id="ed22b-181">d.</span></span>  <span data-ttu-id="ed22b-182">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="ed22b-183">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ed22b-183">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ed22b-185">На hello **конфигурации TimeOffManager** щелкните **Настройка TimeOffManager** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ed22b-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ed22b-186">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ed22b-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Раздел "Конфигурация TimeOffManager"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="ed22b-188">В другом окне веб-браузера войдите на свой корпоративный веб-сайт TimeOffManager в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ed22b-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="ed22b-189">Go слишком**учетной записи \> параметры учетной записи \> параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="ed22b-190">![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ed22b-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="ed22b-191">В hello **параметры единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ed22b-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="ed22b-192">![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ed22b-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="ed22b-193">а.</span><span class="sxs-lookup"><span data-stu-id="ed22b-193">a.</span></span> <span data-ttu-id="ed22b-194">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="ed22b-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="ed22b-195">b.</span><span class="sxs-lookup"><span data-stu-id="ed22b-195">b.</span></span> <span data-ttu-id="ed22b-196">В **издатель Idp** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed22b-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="ed22b-197">c.</span><span class="sxs-lookup"><span data-stu-id="ed22b-197">c.</span></span> <span data-ttu-id="ed22b-198">В **URL-адрес конечной точки поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed22b-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="ed22b-199">d.</span><span class="sxs-lookup"><span data-stu-id="ed22b-199">d.</span></span> <span data-ttu-id="ed22b-200">Для параметра **Enforce SAML** (Применить SAML) выберите значение **No** (Нет).</span><span class="sxs-lookup"><span data-stu-id="ed22b-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="ed22b-201">д.</span><span class="sxs-lookup"><span data-stu-id="ed22b-201">e.</span></span> <span data-ttu-id="ed22b-202">Для параметра **Auto-Create Users** (Автосоздание пользователей) выберите значение **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="ed22b-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="ed22b-203">f.</span><span class="sxs-lookup"><span data-stu-id="ed22b-203">f.</span></span> <span data-ttu-id="ed22b-204">В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ed22b-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="ed22b-205">ж.</span><span class="sxs-lookup"><span data-stu-id="ed22b-205">g.</span></span> <span data-ttu-id="ed22b-206">Нажмите кнопку **Save Changes** (Сохранить изменения).</span><span class="sxs-lookup"><span data-stu-id="ed22b-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="ed22b-207">В **параметры единого входа** страницы значение hello копирования **URL-адрес службы утверждения потребителя** и вставьте его в hello **URL-адрес ответа** текстовое поле под **TimeOffManager URL-адреса и домена** раздела на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ed22b-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="ed22b-208">![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ed22b-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="ed22b-209">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ed22b-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed22b-210">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ed22b-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed22b-211">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed22b-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ed22b-212">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed22b-212">Create an Azure AD test user</span></span>
<span data-ttu-id="ed22b-213">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ed22b-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ed22b-215">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed22b-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed22b-216">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ed22b-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed22b-218">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Пользователи и группы" > "Все пользователи"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed22b-220">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ed22b-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed22b-222">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ed22b-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed22b-224">а.</span><span class="sxs-lookup"><span data-stu-id="ed22b-224">a.</span></span> <span data-ttu-id="ed22b-225">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed22b-226">b.</span><span class="sxs-lookup"><span data-stu-id="ed22b-226">b.</span></span> <span data-ttu-id="ed22b-227">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed22b-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed22b-228">c.</span><span class="sxs-lookup"><span data-stu-id="ed22b-228">c.</span></span> <span data-ttu-id="ed22b-229">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ed22b-230">d.</span><span class="sxs-lookup"><span data-stu-id="ed22b-230">d.</span></span> <span data-ttu-id="ed22b-231">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="ed22b-232">Создание тестового пользователя TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="ed22b-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="ed22b-233">В порядке tooenable toolog пользователей Azure AD в TimeOffManager они должны быть подготовленных tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="ed22b-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="ed22b-234">TimeOffManager поддерживает автоматическую подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="ed22b-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="ed22b-235">С вашей стороны никакие действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="ed22b-235">There is no action item for you.</span></span>  

<span data-ttu-id="ed22b-236">Hello пользователи добавляются автоматически во время первого входа hello единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed22b-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="ed22b-237">Можно использовать любые другие TimeOffManager пользователя средства создания учетных записей или интерфейсы API, предоставляемые TimeOffManager tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed22b-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ed22b-238">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ed22b-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ed22b-239">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTimeOffManager доступа.</span><span class="sxs-lookup"><span data-stu-id="ed22b-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ed22b-241">**tooassign tooTimeOffManager Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ed22b-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed22b-242">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ed22b-244">В списке приложений hello выберите **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager в списке приложений](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="ed22b-246">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ed22b-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-248">Click **Add** button.</span></span> <span data-ttu-id="ed22b-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ed22b-251">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ed22b-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed22b-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed22b-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ed22b-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ed22b-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ed22b-254">Test single sign-on</span></span>

<span data-ttu-id="ed22b-255">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ed22b-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ed22b-256">При нажатии кнопки hello TimeOffManager плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="ed22b-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="ed22b-257">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed22b-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed22b-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ed22b-258">Additional resources</span></span>

* [<span data-ttu-id="ed22b-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed22b-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed22b-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed22b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

