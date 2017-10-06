---
title: "Руководство по интеграции Azure Active Directory с QuickHelp | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="f556f-103">Руководство. Интеграция Azure Active Directory с QuickHelp</span><span class="sxs-lookup"><span data-stu-id="f556f-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="f556f-104">В этом учебнике вы узнаете, как toointegrate QuickHelp с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f556f-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f556f-105">Интеграция с Azure AD QuickHelp предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f556f-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f556f-106">Можно управлять в Azure AD, имеющего доступ tooQuickHelp</span><span class="sxs-lookup"><span data-stu-id="f556f-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="f556f-107">Можно включить на пользователей tooautomatically get вошедшего tooQuickHelp (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f556f-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f556f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f556f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f556f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f556f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f556f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f556f-110">Prerequisites</span></span>

<span data-ttu-id="f556f-111">tooconfigure интеграция Azure AD с QuickHelp требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f556f-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="f556f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f556f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f556f-113">подписка QuickHelp с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f556f-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f556f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f556f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f556f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f556f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f556f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f556f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f556f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f556f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f556f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f556f-118">Scenario description</span></span>
<span data-ttu-id="f556f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f556f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f556f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f556f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f556f-121">Добавление QuickHelp из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f556f-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="f556f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f556f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="f556f-123">Добавление QuickHelp из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f556f-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="f556f-124">tooconfigure hello интеграции QuickHelp в Azure AD, вы должны tooadd QuickHelp из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f556f-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f556f-125">**tooadd QuickHelp из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f556f-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f556f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f556f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f556f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f556f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f556f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f556f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f556f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f556f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f556f-133">Введите в поле поиска hello **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="f556f-133">In hello search box, type **QuickHelp**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="f556f-135">В панели результатов hello выберите **QuickHelp**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f556f-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f556f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f556f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f556f-138">В этом разделе описана настройка и проверка единого входа Azure AD в QuickHelp с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f556f-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f556f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в QuickHelp является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f556f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="f556f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в QuickHelp должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f556f-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="f556f-141">В QuickHelp, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f556f-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f556f-142">tooconfigure и теста Azure AD единого входа с QuickHelp, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f556f-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f556f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f556f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f556f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f556f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f556f-145">**[Создание тестового пользователя QuickHelp](#creating-a-quickhelp-test-user)**  -toohave аналог Саймон Britta в QuickHelp, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f556f-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f556f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f556f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f556f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f556f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f556f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f556f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f556f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="f556f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="f556f-150">**tooconfigure Azure AD единого входа с QuickHelp, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f556f-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="f556f-151">В hello в hello портала Azure **QuickHelp** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f556f-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f556f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f556f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="f556f-155">На hello **URL-адреса и домена QuickHelp** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f556f-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="f556f-157">а.</span><span class="sxs-lookup"><span data-stu-id="f556f-157">a.</span></span> <span data-ttu-id="f556f-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="f556f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="f556f-159">b.</span><span class="sxs-lookup"><span data-stu-id="f556f-159">b.</span></span> <span data-ttu-id="f556f-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="f556f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f556f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f556f-161">These values are not real.</span></span> <span data-ttu-id="f556f-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f556f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f556f-163">Обратитесь к [группа поддержки клиента QuickHelp](https://support.quickhelp.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f556f-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f556f-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f556f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="f556f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f556f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="f556f-168">Корпоративный сайт QuickHelp tooyour входа от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="f556f-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="f556f-169">В меню в верхней части hello hello выберите **администратора**.</span><span class="sxs-lookup"><span data-stu-id="f556f-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Настройка единого входа][21]

8. <span data-ttu-id="f556f-171">В hello **администратора QuickHelp** меню, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="f556f-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Настройка единого входа][22]

9. <span data-ttu-id="f556f-173">Щелкните **Authentication Settings**(Параметра аутентификации).</span><span class="sxs-lookup"><span data-stu-id="f556f-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="f556f-174">На hello **параметры проверки подлинности** выполните следующие шаги hello</span><span class="sxs-lookup"><span data-stu-id="f556f-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Настройка единого входа][23]
   
    <span data-ttu-id="f556f-176">а.</span><span class="sxs-lookup"><span data-stu-id="f556f-176">a.</span></span> <span data-ttu-id="f556f-177">Для параметра **SSO Type** (Тип SSO) выберите значение **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="f556f-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="f556f-178">b.</span><span class="sxs-lookup"><span data-stu-id="f556f-178">b.</span></span> <span data-ttu-id="f556f-179">tooupload файл загруженных метаданных в Azure, щелкните **Обзор**перейдите toohello файл, нажмите кнопку Завершить **Отправка метаданных**.</span><span class="sxs-lookup"><span data-stu-id="f556f-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="f556f-180">c.</span><span class="sxs-lookup"><span data-stu-id="f556f-180">c.</span></span> <span data-ttu-id="f556f-181">В hello **электронной почты** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f556f-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="f556f-182">d.</span><span class="sxs-lookup"><span data-stu-id="f556f-182">d.</span></span> <span data-ttu-id="f556f-183">В hello **имя** текстовом `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="f556f-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="f556f-184">д.</span><span class="sxs-lookup"><span data-stu-id="f556f-184">e.</span></span> <span data-ttu-id="f556f-185">В hello **Фамилия** текстовом `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="f556f-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="f556f-186">f.</span><span class="sxs-lookup"><span data-stu-id="f556f-186">f.</span></span> <span data-ttu-id="f556f-187">В hello **действия**, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f556f-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f556f-188">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f556f-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f556f-189">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f556f-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f556f-190">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f556f-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f556f-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f556f-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="f556f-192">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f556f-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f556f-194">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f556f-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f556f-195">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f556f-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f556f-197">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f556f-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f556f-199">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f556f-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f556f-201">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f556f-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f556f-203">а.</span><span class="sxs-lookup"><span data-stu-id="f556f-203">a.</span></span> <span data-ttu-id="f556f-204">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f556f-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f556f-205">b.</span><span class="sxs-lookup"><span data-stu-id="f556f-205">b.</span></span> <span data-ttu-id="f556f-206">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f556f-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f556f-207">c.</span><span class="sxs-lookup"><span data-stu-id="f556f-207">c.</span></span> <span data-ttu-id="f556f-208">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f556f-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f556f-209">d.</span><span class="sxs-lookup"><span data-stu-id="f556f-209">d.</span></span> <span data-ttu-id="f556f-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f556f-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="f556f-211">Создание тестового пользователя QuickHelp</span><span class="sxs-lookup"><span data-stu-id="f556f-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="f556f-212">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="f556f-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="f556f-213">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в QuickHelp tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f556f-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="f556f-214">Другими словами связи между пользователя Azure AD и связанных пользователей hello в QuickHelp должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f556f-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="f556f-215">QuickHelp поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="f556f-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="f556f-216">Это означает, что при необходимости в QuickHelp учетной записи пользователя автоматически создается и hello учетная запись является toohello связанной учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f556f-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="f556f-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="f556f-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f556f-218">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f556f-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f556f-219">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooQuickHelp доступа.</span><span class="sxs-lookup"><span data-stu-id="f556f-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f556f-221">**tooassign tooQuickHelp Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f556f-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="f556f-222">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f556f-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f556f-224">В списке приложений hello выберите **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="f556f-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="f556f-226">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f556f-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f556f-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f556f-228">Click **Add** button.</span></span> <span data-ttu-id="f556f-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f556f-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f556f-231">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f556f-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f556f-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f556f-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f556f-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f556f-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f556f-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f556f-234">Testing single sign-on</span></span>

<span data-ttu-id="f556f-235">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="f556f-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="f556f-236">При нажатии кнопки hello QuickHelp плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour QuickHelp приложения.</span><span class="sxs-lookup"><span data-stu-id="f556f-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f556f-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f556f-237">Additional resources</span></span>

* [<span data-ttu-id="f556f-238">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f556f-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f556f-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f556f-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
