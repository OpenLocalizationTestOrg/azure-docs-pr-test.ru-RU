---
title: "Руководство по интеграции Azure Active Directory с Pingboard | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="7c903-103">Руководство по интеграции Azure Active Directory с Pingboard</span><span class="sxs-lookup"><span data-stu-id="7c903-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="7c903-104">В этом учебнике вы узнаете, как toointegrate Pingboard с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c903-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c903-105">Интеграция с Azure AD Pingboard предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7c903-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c903-106">Можно управлять в Azure AD, имеющего доступ tooPingboard</span><span class="sxs-lookup"><span data-stu-id="7c903-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="7c903-107">Можно включить на пользователей tooautomatically get вошедшего tooPingboard (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c903-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c903-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="7c903-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="7c903-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c903-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c903-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7c903-110">Prerequisites</span></span>

<span data-ttu-id="7c903-111">tooconfigure интеграция Azure AD с Pingboard требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7c903-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="7c903-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7c903-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c903-113">подписка Pingboard с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7c903-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c903-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7c903-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c903-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7c903-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c903-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="7c903-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7c903-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c903-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c903-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7c903-118">Scenario description</span></span>
<span data-ttu-id="7c903-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7c903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c903-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7c903-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c903-121">Добавление Pingboard из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7c903-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="7c903-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c903-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="7c903-123">Добавление Pingboard из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7c903-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="7c903-124">tooconfigure hello интеграции Pingboard в Azure AD, вы должны tooadd Pingboard из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7c903-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c903-125">**tooadd Pingboard из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7c903-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c903-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7c903-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c903-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7c903-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c903-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7c903-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7c903-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7c903-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7c903-133">Введите в поле поиска hello **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="7c903-133">In hello search box, type **Pingboard**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="7c903-135">В панели результатов hello выберите **Pingboard**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7c903-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c903-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c903-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c903-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Pingboard с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c903-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c903-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Pingboard является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c903-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="7c903-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Pingboard должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7c903-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="7c903-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7c903-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="7c903-142">tooconfigure и теста Azure AD единого входа с Pingboard, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7c903-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c903-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7c903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c903-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7c903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c903-145">**[Создание тестового пользователя Pingboard](#creating-a-pingboard-test-user)**  -toohave аналог Саймон Britta в Pingboard, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="7c903-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7c903-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7c903-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c903-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7c903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c903-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c903-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c903-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7c903-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="7c903-150">**tooconfigure Azure AD единого входа с Pingboard, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7c903-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c903-151">На портале управления Azure hello на hello **Pingboard** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7c903-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7c903-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7c903-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="7c903-155">На hello **Pingboard доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7c903-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="7c903-157">а.</span><span class="sxs-lookup"><span data-stu-id="7c903-157">a.</span></span> <span data-ttu-id="7c903-158">В hello **идентификатор** текстовое поле, значение типа hello как:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="7c903-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="7c903-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c903-159">b.</span></span> <span data-ttu-id="7c903-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="7c903-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c903-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="7c903-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="7c903-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7c903-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7c903-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7c903-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="7c903-164">Обратитесь к [группа поддержки клиента Pingboard](https://support.pingboard.com/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="7c903-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="7c903-165">Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="7c903-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="7c903-167">а.</span><span class="sxs-lookup"><span data-stu-id="7c903-167">a.</span></span> <span data-ttu-id="7c903-168">В hello **URL-адрес входа** текстовое поле, значение типа hello как:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="7c903-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="7c903-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7c903-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="7c903-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7c903-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7c903-173">tooconfigure единого входа на стороне Pingboard, откройте новое окно браузера и войдите в tooyour Pingboard учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7c903-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="7c903-174">Tooset администратора Pingboard копирование единый вход должен быть на.</span><span class="sxs-lookup"><span data-stu-id="7c903-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="7c903-175">Hello верхней строке меню выберите **приложений > интеграции**</span><span class="sxs-lookup"><span data-stu-id="7c903-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="7c903-177">На hello **интеграции** найдите hello **«Azure Active Directory»** плитки и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="7c903-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="7c903-179">В hello модальное далее щелкните **«Настройка»**</span><span class="sxs-lookup"><span data-stu-id="7c903-179">In hello modal that follows click **"Configure"**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="7c903-181">На странице hello можно заметить «интеграция единого входа Azure включения.».</span><span class="sxs-lookup"><span data-stu-id="7c903-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="7c903-182">Откройте hello загружен файл метаданных XML в Блокнот и вставьте hello, содержимого в **метаданные поставщика Удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="7c903-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="7c903-184">файл Hello будет проверяться, и если все работает правильно, будет включен единый вход</span><span class="sxs-lookup"><span data-stu-id="7c903-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c903-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c903-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c903-186">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7c903-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7c903-188">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7c903-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c903-189">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7c903-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c903-191">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="7c903-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c903-193">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7c903-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c903-195">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7c903-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c903-197">а.</span><span class="sxs-lookup"><span data-stu-id="7c903-197">a.</span></span> <span data-ttu-id="7c903-198">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c903-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c903-199">b.</span><span class="sxs-lookup"><span data-stu-id="7c903-199">b.</span></span> <span data-ttu-id="7c903-200">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7c903-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c903-201">c.</span><span class="sxs-lookup"><span data-stu-id="7c903-201">c.</span></span> <span data-ttu-id="7c903-202">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7c903-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c903-203">d.</span><span class="sxs-lookup"><span data-stu-id="7c903-203">d.</span></span> <span data-ttu-id="7c903-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7c903-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="7c903-205">Создание тестового пользователя Pingboard</span><span class="sxs-lookup"><span data-stu-id="7c903-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="7c903-206">В порядке tooenable toolog пользователей Azure AD в Pingboard их необходимо подготовить в Pingboard.</span><span class="sxs-lookup"><span data-stu-id="7c903-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="7c903-207">В случае Pingboard hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="7c903-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="7c903-208">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="7c903-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c903-209">Войдите в систему tooyour Pingboard сайт компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="7c903-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="7c903-210">Нажмите кнопку **Add Employee** (Добавить сотрудника) на странице **Directory** (Каталог).</span><span class="sxs-lookup"><span data-stu-id="7c903-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="7c903-212">На hello **«Добавить сотрудника»** диалогового окна выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7c903-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="7c903-214">а.</span><span class="sxs-lookup"><span data-stu-id="7c903-214">a.</span></span> <span data-ttu-id="7c903-215">В hello **полное имя** textbox hello полное имя типа Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7c903-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="7c903-216">b.</span><span class="sxs-lookup"><span data-stu-id="7c903-216">b.</span></span> <span data-ttu-id="7c903-217">В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7c903-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="7c903-218">c.</span><span class="sxs-lookup"><span data-stu-id="7c903-218">c.</span></span> <span data-ttu-id="7c903-219">В hello **должность** текстового поля, типа hello должности Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7c903-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="7c903-220">d.</span><span class="sxs-lookup"><span data-stu-id="7c903-220">d.</span></span> <span data-ttu-id="7c903-221">В hello **расположение** раскрывающийся список, выберите hello расположение Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7c903-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="7c903-222">д.</span><span class="sxs-lookup"><span data-stu-id="7c903-222">e.</span></span> <span data-ttu-id="7c903-223">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7c903-223">Click **Add**.</span></span>   

4. <span data-ttu-id="7c903-224">Экран подтверждения запустится tooconfirm hello Добавление пользователя.</span><span class="sxs-lookup"><span data-stu-id="7c903-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![Подтверждение](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="7c903-226">Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="7c903-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c903-227">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7c903-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c903-228">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooPingboard доступа.</span><span class="sxs-lookup"><span data-stu-id="7c903-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7c903-230">**tooassign tooPingboard Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7c903-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c903-231">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7c903-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7c903-233">В списке приложений hello выберите **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="7c903-233">In hello applications list, select **Pingboard**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="7c903-235">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7c903-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7c903-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7c903-237">Click **Add** button.</span></span> <span data-ttu-id="7c903-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7c903-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7c903-240">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7c903-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c903-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7c903-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c903-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7c903-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c903-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7c903-243">Testing single sign-on</span></span>

<span data-ttu-id="7c903-244">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7c903-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c903-245">При нажатии кнопки hello Pingboard плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Pingboard приложения.</span><span class="sxs-lookup"><span data-stu-id="7c903-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c903-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7c903-246">Additional resources</span></span>

* [<span data-ttu-id="7c903-247">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c903-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c903-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c903-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
