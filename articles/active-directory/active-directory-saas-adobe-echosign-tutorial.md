---
title: "Руководство по интеграции Azure Active Directory с Adobe Sign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Adobe знаком."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="b9264-103">Руководство по интеграции Azure Active Directory с Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="b9264-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="b9264-104">В этом учебнике вы узнаете, как Adobe toointegrate, войдите в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9264-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9264-105">Интеграция с Azure AD входа Adobe предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b9264-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9264-106">Можно управлять в Azure AD, имеющего доступ tooAdobe входа</span><span class="sxs-lookup"><span data-stu-id="b9264-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="b9264-107">Можно включить на пользователей tooautomatically get вошедшего tooAdobe входа (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9264-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9264-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b9264-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9264-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9264-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9264-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9264-110">Prerequisites</span></span>

<span data-ttu-id="b9264-111">tooconfigure интеграция Azure AD с Adobe входа требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b9264-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="b9264-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b9264-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9264-113">подписка Adobe Sign с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9264-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9264-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b9264-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9264-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b9264-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9264-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b9264-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9264-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9264-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9264-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b9264-118">Scenario description</span></span>
<span data-ttu-id="b9264-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b9264-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9264-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b9264-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9264-121">Добавление входа Adobe из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9264-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="b9264-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9264-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="b9264-123">Добавление входа Adobe из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b9264-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="b9264-124">tooconfigure hello интеграции Adobe входа в Azure AD, вы должны tooadd входа Adobe из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9264-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9264-125">**tooadd входа Adobe из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9264-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9264-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9264-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9264-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b9264-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9264-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9264-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b9264-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b9264-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b9264-133">Введите в поле поиска hello **входа Adobe**.</span><span class="sxs-lookup"><span data-stu-id="b9264-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="b9264-135">В панели результатов hello выберите **входа Adobe**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b9264-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9264-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9264-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9264-138">В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Sign с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9264-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9264-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Adobe входа является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9264-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="b9264-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Adobe входа должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b9264-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="b9264-141">В Adobe знака, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b9264-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9264-142">tooconfigure и теста Azure AD единого входа с Adobe входа, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9264-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9264-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b9264-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9264-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b9264-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9264-145">**[Создание тестового пользователя, прошедшего входа Adobe](#creating-an-adobe-sign-test-user)**  -toohave аналог Саймон Britta в Adobe знак, который является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b9264-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9264-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b9264-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9264-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b9264-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9264-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9264-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9264-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Adobe входа.</span><span class="sxs-lookup"><span data-stu-id="b9264-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="b9264-150">**Azure AD tooconfigure единого входа с входа Adobe выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="b9264-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9264-151">В hello в hello портала Azure **входа Adobe** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b9264-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b9264-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b9264-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="b9264-155">На hello **URL-адреса и домена входа Adobe** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9264-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="b9264-157">а.</span><span class="sxs-lookup"><span data-stu-id="b9264-157">a.</span></span> <span data-ttu-id="b9264-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="b9264-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="b9264-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9264-159">b.</span></span> <span data-ttu-id="b9264-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="b9264-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9264-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b9264-161">These values are not real.</span></span> <span data-ttu-id="b9264-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b9264-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9264-163">Обратитесь к [группа поддержки клиента входа Adobe](https://helpx.adobe.com/in/contact/support.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b9264-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9264-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b9264-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="b9264-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b9264-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9264-168">На hello **конфигурации входа Adobe** щелкните **входа Adobe Настройка** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b9264-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9264-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b9264-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="b9264-171">В другом окне браузера Войдите на сайте компании tooyour входа Adobe в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b9264-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="b9264-172">В меню в верхней части hello hello выберите **учетной записи**, hello hello левой панели навигации нажмите кнопку **параметры SAML** под **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="b9264-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="b9264-173">![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Учетная запись")</span><span class="sxs-lookup"><span data-stu-id="b9264-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="b9264-174">В hello в разделе "Параметры SAML" выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b9264-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b9264-175">![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="b9264-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="b9264-176">а.</span><span class="sxs-lookup"><span data-stu-id="b9264-176">a.</span></span> <span data-ttu-id="b9264-177">В разделе **SAML Mode** (Режим SAML) выберите параметр **SAML Mandatory** (SAML обязательно).</span><span class="sxs-lookup"><span data-stu-id="b9264-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="b9264-178">b.</span><span class="sxs-lookup"><span data-stu-id="b9264-178">b.</span></span> <span data-ttu-id="b9264-179">Выберите **toolog Разрешить администраторам учетных записей EchoSign с помощью учетных данных EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="b9264-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="b9264-180">c.</span><span class="sxs-lookup"><span data-stu-id="b9264-180">c.</span></span> <span data-ttu-id="b9264-181">В разделе **User Creation** (Создание пользователей) установите флажок **Automatically add users authenticated through SAML** (Автоматически добавлять пользователей, прошедших проверку подлинности с использованием SAML).</span><span class="sxs-lookup"><span data-stu-id="b9264-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="b9264-182">Продолжите и выполнении hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b9264-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="b9264-183">![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="b9264-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="b9264-184">а.</span><span class="sxs-lookup"><span data-stu-id="b9264-184">a.</span></span> <span data-ttu-id="b9264-185">Вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure в hello **идентификатор сущности поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b9264-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="b9264-186">b.</span><span class="sxs-lookup"><span data-stu-id="b9264-186">b.</span></span> <span data-ttu-id="b9264-187">Вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b9264-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="b9264-188">c.</span><span class="sxs-lookup"><span data-stu-id="b9264-188">c.</span></span> <span data-ttu-id="b9264-189">Вставить **URL-адрес выхода**, который вы скопировали из портала Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b9264-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="b9264-190">d.</span><span class="sxs-lookup"><span data-stu-id="b9264-190">d.</span></span> <span data-ttu-id="b9264-191">Откройте ваш загруженный **Certificate(Base64)** в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля</span><span class="sxs-lookup"><span data-stu-id="b9264-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="b9264-192">д.</span><span class="sxs-lookup"><span data-stu-id="b9264-192">e.</span></span> <span data-ttu-id="b9264-193">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="b9264-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b9264-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b9264-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9264-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b9264-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9264-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9264-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9264-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9264-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9264-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b9264-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b9264-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9264-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9264-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b9264-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9264-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b9264-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9264-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b9264-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9264-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9264-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9264-209">а.</span><span class="sxs-lookup"><span data-stu-id="b9264-209">a.</span></span> <span data-ttu-id="b9264-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9264-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9264-211">b.</span><span class="sxs-lookup"><span data-stu-id="b9264-211">b.</span></span> <span data-ttu-id="b9264-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9264-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9264-213">c.</span><span class="sxs-lookup"><span data-stu-id="b9264-213">c.</span></span> <span data-ttu-id="b9264-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b9264-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9264-215">d.</span><span class="sxs-lookup"><span data-stu-id="b9264-215">d.</span></span> <span data-ttu-id="b9264-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b9264-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="b9264-217">Создание тестового пользователя Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="b9264-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="b9264-218">Пользователи toolog tooenable Azure AD в tooAdobe входа, их необходимо подготовить в Adobe входа.</span><span class="sxs-lookup"><span data-stu-id="b9264-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="b9264-219">В случае hello входа Adobe Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b9264-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b9264-220">Можно использовать любые другие Adobe входа пользователя средства создания учетных записей или интерфейсы API, предоставляемые tooprovision входа Adobe учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="b9264-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="b9264-221">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9264-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9264-222">Войдите в tooyour **входа Adobe** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b9264-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="b9264-223">В меню в верхней части hello hello выберите **учетной записи**, hello hello левой панели навигации нажмите кнопку **пользователи и группы**и нажмите кнопку **создать нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b9264-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="b9264-224">![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Учетная запись")</span><span class="sxs-lookup"><span data-stu-id="b9264-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="b9264-225">В hello **создать нового пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b9264-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="b9264-226">![Создание пользователя](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="b9264-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="b9264-227">а.</span><span class="sxs-lookup"><span data-stu-id="b9264-227">a.</span></span> <span data-ttu-id="b9264-228">Тип hello **адрес электронной почты**, **имя**, и **Фамилия** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="b9264-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="b9264-229">b.</span><span class="sxs-lookup"><span data-stu-id="b9264-229">b.</span></span> <span data-ttu-id="b9264-230">Нажмите кнопку **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b9264-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="b9264-231">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="b9264-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9264-232">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b9264-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9264-233">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAdobe входа.</span><span class="sxs-lookup"><span data-stu-id="b9264-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b9264-235">**tooassign tooAdobe Britta Simon входа, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b9264-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9264-236">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b9264-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b9264-238">В списке приложений hello выберите **входа Adobe**.</span><span class="sxs-lookup"><span data-stu-id="b9264-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="b9264-240">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b9264-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b9264-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b9264-242">Click **Add** button.</span></span> <span data-ttu-id="b9264-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b9264-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b9264-245">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b9264-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9264-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b9264-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9264-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b9264-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9264-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b9264-248">Testing single sign-on</span></span>

<span data-ttu-id="b9264-249">При нажатии кнопки входа Adobe плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour входа Adobe приложения.</span><span class="sxs-lookup"><span data-stu-id="b9264-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="b9264-250">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9264-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9264-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9264-251">Additional resources</span></span>

* [<span data-ttu-id="b9264-252">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9264-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9264-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9264-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

