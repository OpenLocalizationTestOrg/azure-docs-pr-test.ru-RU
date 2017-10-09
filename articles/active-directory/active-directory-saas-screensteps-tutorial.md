---
title: "Руководство по интеграции Azure Active Directory с ScreenSteps | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="63ba0-103">Учебник. Интеграция Azure Active Directory с ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="63ba0-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="63ba0-104">В этом учебнике вы узнаете, как toointegrate ScreenSteps с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63ba0-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63ba0-105">Интеграция ScreenSteps с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="63ba0-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63ba0-106">Можно управлять в Azure AD, имеющего доступ tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="63ba0-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="63ba0-107">Можно включить на пользователей tooautomatically get вошедшего tooScreenSteps (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63ba0-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="63ba0-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="63ba0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="63ba0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63ba0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63ba0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="63ba0-110">Prerequisites</span></span>

<span data-ttu-id="63ba0-111">tooconfigure интеграция Azure AD с ScreenSteps требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="63ba0-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="63ba0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="63ba0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63ba0-113">подписка ScreenSteps с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="63ba0-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63ba0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="63ba0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63ba0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="63ba0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63ba0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="63ba0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63ba0-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63ba0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63ba0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="63ba0-118">Scenario description</span></span>
<span data-ttu-id="63ba0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="63ba0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63ba0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="63ba0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63ba0-121">Добавление ScreenSteps из галереи hello</span><span class="sxs-lookup"><span data-stu-id="63ba0-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="63ba0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ba0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="63ba0-123">Добавление ScreenSteps из галереи hello</span><span class="sxs-lookup"><span data-stu-id="63ba0-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="63ba0-124">tooconfigure hello интеграции ScreenSteps в Azure AD, вы должны tooadd ScreenSteps из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="63ba0-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63ba0-125">**tooadd ScreenSteps из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="63ba0-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ba0-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="63ba0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="63ba0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63ba0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="63ba0-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="63ba0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="63ba0-133">Введите в поле поиска hello **ScreenSteps**выберите **ScreenSteps** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="63ba0-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps в списке результатов hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="63ba0-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ba0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="63ba0-136">В этом разделе описана настройка и проверка единого входа Azure AD в ScreenSteps с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63ba0-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63ba0-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ScreenSteps является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63ba0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="63ba0-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в ScreenSteps должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="63ba0-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="63ba0-139">В ScreenSteps, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="63ba0-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63ba0-140">tooconfigure и теста Azure AD единого входа с ScreenSteps, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="63ba0-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63ba0-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="63ba0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63ba0-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="63ba0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63ba0-143">**[Создание тестового пользователя ScreenSteps](#create-a-screensteps-test-user) ** -toohave аналог Саймон Britta в ScreenSteps, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="63ba0-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63ba0-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="63ba0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63ba0-145">**[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63ba0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="63ba0-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ba0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="63ba0-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ScreenSteps приложения.</span><span class="sxs-lookup"><span data-stu-id="63ba0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="63ba0-148">**tooconfigure Azure AD единого входа с ScreenSteps, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="63ba0-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ba0-149">В hello в hello портала Azure **ScreenSteps** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="63ba0-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="63ba0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="63ba0-153">На hello **URL-адреса и домена ScreenSteps** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="63ba0-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="63ba0-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="63ba0-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63ba0-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="63ba0-156">This value is not real.</span></span> <span data-ttu-id="63ba0-157">Измените значение этого параметра hello фактический URL-адрес входа, который описывается далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="63ba0-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="63ba0-158">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="63ba0-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="63ba0-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="63ba0-160">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63ba0-162">На hello **конфигурации ScreenSteps** щелкните **Настройка ScreenSteps** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="63ba0-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="63ba0-163">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="63ba0-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="63ba0-165">В другом окне веб-браузера войдите на сайт ScreenSteps своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="63ba0-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="63ba0-166">Щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="63ba0-167">![Управление учетными записями](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Управление учетными записями")</span><span class="sxs-lookup"><span data-stu-id="63ba0-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="63ba0-168">Щелкните **Single Sign-on**(Единый вход).</span><span class="sxs-lookup"><span data-stu-id="63ba0-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="63ba0-169">![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Удаленная аутентификация")</span><span class="sxs-lookup"><span data-stu-id="63ba0-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="63ba0-170">Щелкните **Create Single Sign-on Endpoint** (Создать конечную точку единого входа).</span><span class="sxs-lookup"><span data-stu-id="63ba0-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="63ba0-171">![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Удаленная аутентификация")</span><span class="sxs-lookup"><span data-stu-id="63ba0-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="63ba0-172">В hello **создать единую конечную точку входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="63ba0-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="63ba0-173">![Создание конечной точки аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Создание конечной точки аутентификации")</span><span class="sxs-lookup"><span data-stu-id="63ba0-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="63ba0-174">а.</span><span class="sxs-lookup"><span data-stu-id="63ba0-174">a.</span></span> <span data-ttu-id="63ba0-175">В hello **заголовок** текстовом поле введите заголовок.</span><span class="sxs-lookup"><span data-stu-id="63ba0-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="63ba0-176">b.</span><span class="sxs-lookup"><span data-stu-id="63ba0-176">b.</span></span> <span data-ttu-id="63ba0-177">Из hello **режим** выберите **SAML**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="63ba0-178">c.</span><span class="sxs-lookup"><span data-stu-id="63ba0-178">c.</span></span> <span data-ttu-id="63ba0-179">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-179">Click **Create**.</span></span>

12. <span data-ttu-id="63ba0-180">**Изменить** hello новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="63ba0-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="63ba0-181">![Изменение конечной точки](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span><span class="sxs-lookup"><span data-stu-id="63ba0-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="63ba0-182">В hello **изменить одну конечную точку входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="63ba0-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="63ba0-183">![Конечная точка удаленной аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Конечная точка удаленной аутентификации")</span><span class="sxs-lookup"><span data-stu-id="63ba0-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="63ba0-184">а.</span><span class="sxs-lookup"><span data-stu-id="63ba0-184">a.</span></span> <span data-ttu-id="63ba0-185">Нажмите кнопку **передачи новый файл сертификата SAML**, а затем передачи hello сертификат, который вы скачали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="63ba0-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="63ba0-186">b.</span><span class="sxs-lookup"><span data-stu-id="63ba0-186">b.</span></span> <span data-ttu-id="63ba0-187">Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес удаленного входа** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="63ba0-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="63ba0-188">c.</span><span class="sxs-lookup"><span data-stu-id="63ba0-188">c.</span></span> <span data-ttu-id="63ba0-189">Вставить **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="63ba0-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="63ba0-190">d.</span><span class="sxs-lookup"><span data-stu-id="63ba0-190">d.</span></span> <span data-ttu-id="63ba0-191">Выберите **группы** toowhen tooassign пользователей, их инициализации.</span><span class="sxs-lookup"><span data-stu-id="63ba0-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="63ba0-192">д.</span><span class="sxs-lookup"><span data-stu-id="63ba0-192">e.</span></span> <span data-ttu-id="63ba0-193">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-193">Click **Update**.</span></span>

    <span data-ttu-id="63ba0-194">f.</span><span class="sxs-lookup"><span data-stu-id="63ba0-194">f.</span></span> <span data-ttu-id="63ba0-195">Hello копирования **URL-адрес потребителя SAML** toohello буфер обмена и вставьте в toohello **URL-адрес входа** текстовое поле в **URL-адреса и домена ScreenSteps** раздела.</span><span class="sxs-lookup"><span data-stu-id="63ba0-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="63ba0-196">ж.</span><span class="sxs-lookup"><span data-stu-id="63ba0-196">g.</span></span> <span data-ttu-id="63ba0-197">Вернуть toohello **изменить одну конечную точку входа**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="63ba0-198">h.</span><span class="sxs-lookup"><span data-stu-id="63ba0-198">h.</span></span> <span data-ttu-id="63ba0-199">Нажмите кнопку hello **сделать по умолчанию для учетной записи** кнопку toouse эту конечную точку для всех пользователей, входящих в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="63ba0-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="63ba0-200">Кроме того, можно щелкнуть hello **добавить tooSite** кнопку toouse эту конечную точку для определенных сайтов в **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="63ba0-201">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="63ba0-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63ba0-202">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="63ba0-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63ba0-203">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63ba0-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="63ba0-204">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ba0-204">Create an Azure AD test user</span></span>

<span data-ttu-id="63ba0-205">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="63ba0-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="63ba0-207">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="63ba0-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ba0-208">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="63ba0-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="63ba0-210">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="63ba0-212">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="63ba0-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="63ba0-214">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="63ba0-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="63ba0-216">а.</span><span class="sxs-lookup"><span data-stu-id="63ba0-216">a.</span></span> <span data-ttu-id="63ba0-217">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63ba0-218">b.</span><span class="sxs-lookup"><span data-stu-id="63ba0-218">b.</span></span> <span data-ttu-id="63ba0-219">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="63ba0-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="63ba0-220">c.</span><span class="sxs-lookup"><span data-stu-id="63ba0-220">c.</span></span> <span data-ttu-id="63ba0-221">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="63ba0-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="63ba0-222">d.</span><span class="sxs-lookup"><span data-stu-id="63ba0-222">d.</span></span> <span data-ttu-id="63ba0-223">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="63ba0-224">Создание тестового пользователя ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="63ba0-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="63ba0-225">В этом разделе описано, как создать пользователя Britta Simon в ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="63ba0-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="63ba0-226">Работать с [группа поддержки клиент ScreenSteps](https://www.screensteps.com/contact) для добавления пользователей hello в платформе ScreenSteps hello.</span><span class="sxs-lookup"><span data-stu-id="63ba0-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="63ba0-227">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="63ba0-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="63ba0-228">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="63ba0-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="63ba0-229">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooScreenSteps доступа.</span><span class="sxs-lookup"><span data-stu-id="63ba0-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="63ba0-231">**tooassign tooScreenSteps Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="63ba0-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="63ba0-232">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="63ba0-234">В списке приложений hello выберите **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![ссылка ScreenSteps Hello в списке приложений hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="63ba0-236">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="63ba0-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-238">Click **Add** button.</span></span> <span data-ttu-id="63ba0-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="63ba0-241">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="63ba0-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63ba0-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63ba0-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="63ba0-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="63ba0-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="63ba0-244">Test single sign-on</span></span>

<span data-ttu-id="63ba0-245">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="63ba0-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="63ba0-246">При нажатии кнопки ScreenSteps плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour ScreenSteps приложения.</span><span class="sxs-lookup"><span data-stu-id="63ba0-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="63ba0-247">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="63ba0-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="63ba0-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="63ba0-248">Additional resources</span></span>

* [<span data-ttu-id="63ba0-249">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63ba0-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63ba0-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63ba0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

