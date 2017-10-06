---
title: "Руководство по интеграции Azure Active Directory с TalentLMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="7065b-103">Руководство по интеграции Azure Active Directory с TalentLMS</span><span class="sxs-lookup"><span data-stu-id="7065b-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="7065b-104">В этом учебнике вы узнаете, как toointegrate TalentLMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7065b-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7065b-105">Интеграция TalentLMS с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7065b-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7065b-106">Можно управлять в Azure AD, имеющего доступ tooTalentLMS</span><span class="sxs-lookup"><span data-stu-id="7065b-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="7065b-107">Можно включить на пользователей tooautomatically get вошедшего tooTalentLMS (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7065b-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7065b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7065b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7065b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7065b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7065b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7065b-110">Prerequisites</span></span>

<span data-ttu-id="7065b-111">tooconfigure интеграция Azure AD с TalentLMS требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7065b-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="7065b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7065b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7065b-113">подписка TalentLMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7065b-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7065b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7065b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7065b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7065b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7065b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7065b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7065b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7065b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7065b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7065b-118">Scenario description</span></span>
<span data-ttu-id="7065b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7065b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7065b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7065b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7065b-121">Добавление TalentLMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7065b-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="7065b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7065b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="7065b-123">Добавление TalentLMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7065b-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="7065b-124">tooconfigure hello интеграции TalentLMS в Azure AD, вы должны tooadd TalentLMS из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7065b-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7065b-125">**tooadd TalentLMS из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7065b-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7065b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7065b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7065b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7065b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7065b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7065b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7065b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7065b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7065b-133">Введите в поле поиска hello **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="7065b-133">In hello search box, type **TalentLMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="7065b-135">В панели результатов hello выберите **TalentLMS**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7065b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7065b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7065b-138">В этом разделе описана настройка и проверка единого входа Azure AD в TalentLMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7065b-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7065b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TalentLMS является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7065b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="7065b-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в TalentLMS требуется toobe установлено.</span><span class="sxs-lookup"><span data-stu-id="7065b-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="7065b-141">В TalentLMS, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7065b-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7065b-142">tooconfigure и теста Azure AD единого входа с TalentLMS, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7065b-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7065b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7065b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7065b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7065b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7065b-145">**[Создание тестового пользователя TalentLMS](#creating-a-talentlms-test-user)**  -toohave аналог Саймон Britta в TalentLMS, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7065b-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7065b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7065b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7065b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7065b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7065b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7065b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7065b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в TalentLMS приложения.</span><span class="sxs-lookup"><span data-stu-id="7065b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="7065b-150">**Azure AD tooconfigure единого входа с TalentLMS, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7065b-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7065b-151">В hello в hello портала Azure **TalentLMS** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7065b-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7065b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7065b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="7065b-155">На hello **URL-адреса и домена TalentLMS** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7065b-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="7065b-157">а.</span><span class="sxs-lookup"><span data-stu-id="7065b-157">a.</span></span> <span data-ttu-id="7065b-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="7065b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="7065b-159">b.</span><span class="sxs-lookup"><span data-stu-id="7065b-159">b.</span></span> <span data-ttu-id="7065b-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="7065b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7065b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7065b-161">These values are not real.</span></span> <span data-ttu-id="7065b-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7065b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7065b-163">Обратитесь к [группа поддержки клиент TalentLMS](https://www.talentlms.com/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="7065b-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="7065b-164">На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение на основе сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="7065b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7065b-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7065b-168">На hello **конфигурации TalentLMS** щелкните **Настройка TalentLMS** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="7065b-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7065b-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="7065b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="7065b-171">В другом окне браузера войти в корпоративный сайт TalentLMS tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7065b-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="7065b-172">В hello **учетная запись и параметры** щелкните hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7065b-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="7065b-173">![Учетная запись и параметры](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Учетная запись и параметры")</span><span class="sxs-lookup"><span data-stu-id="7065b-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="7065b-174">Щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7065b-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="7065b-175">В hello единым входом раздел выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7065b-176">![Единый вход](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7065b-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="7065b-177">а.</span><span class="sxs-lookup"><span data-stu-id="7065b-177">a.</span></span> <span data-ttu-id="7065b-178">Из hello **тип интеграции единого входа** выберите **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7065b-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="7065b-179">b.</span><span class="sxs-lookup"><span data-stu-id="7065b-179">b.</span></span> <span data-ttu-id="7065b-180">В hello **поставщика удостоверений (IDP)** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7065b-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="7065b-181">c.</span><span class="sxs-lookup"><span data-stu-id="7065b-181">c.</span></span> <span data-ttu-id="7065b-182">Вставить hello **отпечаток** значение из портала Azure в hello **отпечаток сертификата** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="7065b-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="7065b-183">d.</span><span class="sxs-lookup"><span data-stu-id="7065b-183">d.</span></span>  <span data-ttu-id="7065b-184">В hello **удаленный URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7065b-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="7065b-185">д.</span><span class="sxs-lookup"><span data-stu-id="7065b-185">e.</span></span> <span data-ttu-id="7065b-186">В hello **URL-адрес удаленного выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7065b-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7065b-187">f.</span><span class="sxs-lookup"><span data-stu-id="7065b-187">f.</span></span> <span data-ttu-id="7065b-188">Заполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="7065b-189">В hello **TargetedID** текстовое поле, тип`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="7065b-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="7065b-190">В hello **имя** текстовое поле, тип`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="7065b-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="7065b-191">В hello **Фамилия** текстовое поле, тип`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="7065b-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="7065b-192">В hello **электронной почты** текстовое поле, тип`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="7065b-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="7065b-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7065b-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="7065b-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7065b-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7065b-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7065b-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7065b-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7065b-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7065b-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="7065b-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7065b-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7065b-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7065b-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7065b-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7065b-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7065b-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7065b-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7065b-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7065b-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7065b-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7065b-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7065b-209">а.</span><span class="sxs-lookup"><span data-stu-id="7065b-209">a.</span></span> <span data-ttu-id="7065b-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7065b-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7065b-211">b.</span><span class="sxs-lookup"><span data-stu-id="7065b-211">b.</span></span> <span data-ttu-id="7065b-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7065b-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7065b-213">c.</span><span class="sxs-lookup"><span data-stu-id="7065b-213">c.</span></span> <span data-ttu-id="7065b-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7065b-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7065b-215">d.</span><span class="sxs-lookup"><span data-stu-id="7065b-215">d.</span></span> <span data-ttu-id="7065b-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7065b-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="7065b-217">Создание тестового пользователя TalentLMS</span><span class="sxs-lookup"><span data-stu-id="7065b-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="7065b-218">Пользователи toolog tooenable Azure AD в tooTalentLMS, их необходимо подготовить в TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="7065b-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="7065b-219">В случае hello TalentLMS Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="7065b-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="7065b-220">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7065b-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7065b-221">Войдите в tooyour **TalentLMS** клиента.</span><span class="sxs-lookup"><span data-stu-id="7065b-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="7065b-222">Щелкните **Пользователи**, а затем — **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="7065b-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="7065b-223">На hello **добавить пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7065b-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="7065b-224">![Добавление пользователя](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="7065b-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="7065b-225">а.</span><span class="sxs-lookup"><span data-stu-id="7065b-225">a.</span></span> <span data-ttu-id="7065b-226">В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7065b-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="7065b-227">b.</span><span class="sxs-lookup"><span data-stu-id="7065b-227">b.</span></span> <span data-ttu-id="7065b-228">В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7065b-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="7065b-229">c.</span><span class="sxs-lookup"><span data-stu-id="7065b-229">c.</span></span> <span data-ttu-id="7065b-230">В hello **адрес электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7065b-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7065b-231">d.</span><span class="sxs-lookup"><span data-stu-id="7065b-231">d.</span></span> <span data-ttu-id="7065b-232">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="7065b-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="7065b-233">Можно использовать любые другие TalentLMS пользователя средства создания учетных записей или интерфейсы API, предоставляемые TalentLMS tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="7065b-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7065b-234">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7065b-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7065b-235">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTalentLMS доступа.</span><span class="sxs-lookup"><span data-stu-id="7065b-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7065b-237">**tooassign tooTalentLMS Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7065b-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7065b-238">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7065b-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7065b-240">В списке приложений hello выберите **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="7065b-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="7065b-242">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7065b-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7065b-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7065b-244">Click **Add** button.</span></span> <span data-ttu-id="7065b-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7065b-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7065b-247">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7065b-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7065b-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7065b-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7065b-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7065b-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7065b-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7065b-250">Testing single sign-on</span></span>

<span data-ttu-id="7065b-251">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="7065b-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7065b-252">При нажатии кнопки TalentLMS плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour TalentLMS приложения</span><span class="sxs-lookup"><span data-stu-id="7065b-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7065b-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7065b-253">Additional resources</span></span>

* [<span data-ttu-id="7065b-254">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7065b-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7065b-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7065b-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

