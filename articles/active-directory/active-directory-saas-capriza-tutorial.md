---
title: "Руководство по интеграции Azure Active Directory с Capriza Platform | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Capriza платформы."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1c4adb737bb5ba4690bbf74688010238c5c83f3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="ee470-103">Руководство по интеграции Azure Active Directory с Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="ee470-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="ee470-104">В этом учебнике вы узнаете, как toointegrate Capriza платформы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee470-104">In this tutorial, you learn how toointegrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee470-105">Интеграция платформы Capriza с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ee470-105">Integrating Capriza Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee470-106">Можно управлять в Azure AD, имеющего доступ tooCapriza платформы</span><span class="sxs-lookup"><span data-stu-id="ee470-106">You can control in Azure AD who has access tooCapriza Platform</span></span>
- <span data-ttu-id="ee470-107">Можно включить на пользователей tooautomatically get вошедшего tooCapriza платформы (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee470-107">You can enable your users tooautomatically get signed-on tooCapriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee470-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ee470-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee470-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee470-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee470-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ee470-110">Prerequisites</span></span>

<span data-ttu-id="ee470-111">tooconfigure интеграция Azure AD с платформой Capriza требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ee470-111">tooconfigure Azure AD integration with Capriza Platform, you need hello following items:</span></span>

- <span data-ttu-id="ee470-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ee470-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee470-113">подписка Capriza Platform с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ee470-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee470-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ee470-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee470-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ee470-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee470-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ee470-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee470-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee470-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee470-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ee470-118">Scenario description</span></span>
<span data-ttu-id="ee470-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ee470-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee470-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ee470-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee470-121">Добавление платформы Capriza из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ee470-121">Adding Capriza Platform from hello gallery</span></span>
2. <span data-ttu-id="ee470-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee470-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-hello-gallery"></a><span data-ttu-id="ee470-123">Добавление платформы Capriza из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ee470-123">Adding Capriza Platform from hello gallery</span></span>
<span data-ttu-id="ee470-124">tooconfigure hello интеграция Capriza платформы в Azure AD, вы должны tooadd Capriza платформы из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ee470-124">tooconfigure hello integration of Capriza Platform into Azure AD, you need tooadd Capriza Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee470-125">**tooadd Capriza платформы из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ee470-125">**tooadd Capriza Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee470-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ee470-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee470-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ee470-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee470-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ee470-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ee470-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ee470-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ee470-133">Введите в поле поиска hello **Capriza платформы**.</span><span class="sxs-lookup"><span data-stu-id="ee470-133">In hello search box, type **Capriza Platform**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="ee470-135">В панели результатов hello выберите **платформы Capriza**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ee470-135">In hello results panel, select **Capriza Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee470-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee470-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee470-138">В этом разделе описана настройка и проверка единого входа Azure AD в Capriza Platform с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee470-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee470-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello Capriza платформы является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee470-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Capriza Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="ee470-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей на платформе Capriza должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ee470-140">In other words, a link relationship between an Azure AD user and hello related user in Capriza Platform needs toobe established.</span></span>

<span data-ttu-id="ee470-141">На платформе Capriza, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ee470-141">In Capriza Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ee470-142">tooconfigure и теста Azure AD единого входа с Capriza платформы, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="ee470-142">tooconfigure and test Azure AD single sign-on with Capriza Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee470-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ee470-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee470-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ee470-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee470-145">**[Создание тестового пользователя платформы Capriza](#creating-a-capriza-platform-test-user)**  -toohave аналог Саймон Britta на платформе Capriza, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee470-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - toohave a counterpart of Britta Simon in Capriza Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee470-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ee470-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee470-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ee470-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee470-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee470-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee470-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Capriza платформы.</span><span class="sxs-lookup"><span data-stu-id="ee470-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="ee470-150">**tooconfigure Azure AD единого входа с платформой Capriza выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee470-150">**tooconfigure Azure AD single sign-on with Capriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee470-151">В hello в hello портала Azure **платформы Capriza** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ee470-151">In hello Azure portal, on hello **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ee470-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ee470-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="ee470-155">На hello **URL-адреса и домена платформы Capriza** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ee470-155">On hello **Capriza Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="ee470-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="ee470-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee470-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ee470-158">This value is not real.</span></span> <span data-ttu-id="ee470-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ee470-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ee470-160">Обратитесь к [группа поддержки клиентских платформ Capriza](mailTo:support@capriza.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="ee470-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) tooget this value.</span></span> 

4. <span data-ttu-id="ee470-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ee470-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="ee470-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ee470-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee470-165">На hello **конфигурации платформы Capriza** щелкните **настройка платформы Capriza** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ee470-165">On hello **Capriza Platform Configuration** section, click **Configure Capriza Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee470-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ee470-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="ee470-168">tooconfigure единого входа на **платформы Capriza** стороны, необходимо загрузить hello toosend **сертификат**, **URL-адрес выхода**, **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** слишком[группа поддержки платформы Capriza](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="ee470-168">tooconfigure single sign-on on **Capriza Platform** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="ee470-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="ee470-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ee470-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ee470-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee470-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ee470-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee470-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee470-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee470-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee470-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee470-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ee470-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ee470-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee470-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee470-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ee470-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee470-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ee470-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee470-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ee470-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee470-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ee470-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee470-185">а.</span><span class="sxs-lookup"><span data-stu-id="ee470-185">a.</span></span> <span data-ttu-id="ee470-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee470-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee470-187">b.</span><span class="sxs-lookup"><span data-stu-id="ee470-187">b.</span></span> <span data-ttu-id="ee470-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee470-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee470-189">c.</span><span class="sxs-lookup"><span data-stu-id="ee470-189">c.</span></span> <span data-ttu-id="ee470-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ee470-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee470-191">d.</span><span class="sxs-lookup"><span data-stu-id="ee470-191">d.</span></span> <span data-ttu-id="ee470-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ee470-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="ee470-193">Создание тестового пользователя Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="ee470-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="ee470-194">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Capriza.</span><span class="sxs-lookup"><span data-stu-id="ee470-194">hello objective of this section is toocreate a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="ee470-195">Приложение Capriza поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ee470-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="ee470-196">**Убедитесь, что ваше доменное имя настроено в Capriza для подготовки пользователей. После этого только hello подготовку пользователей just-in-time будет работать.**</span><span class="sxs-lookup"><span data-stu-id="ee470-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only hello just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="ee470-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="ee470-197">There is no action item for you in this section.</span></span> <span data-ttu-id="ee470-198">Если он еще не существует во время попытки tooaccess Capriza создается новый пользователь.</span><span class="sxs-lookup"><span data-stu-id="ee470-198">A new user will be created during an attempt tooaccess Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee470-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ee470-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee470-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа к tooCapriza платформы.</span><span class="sxs-lookup"><span data-stu-id="ee470-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCapriza Platform.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ee470-202">**tooassign tooCapriza Britta Simon платформы, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ee470-202">**tooassign Britta Simon tooCapriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee470-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ee470-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ee470-205">В списке приложений hello выберите **Capriza платформы**.</span><span class="sxs-lookup"><span data-stu-id="ee470-205">In hello applications list, select **Capriza Platform**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="ee470-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ee470-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ee470-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ee470-209">Click **Add** button.</span></span> <span data-ttu-id="ee470-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ee470-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ee470-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ee470-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee470-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ee470-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee470-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ee470-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee470-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ee470-215">Testing single sign-on</span></span>

<span data-ttu-id="ee470-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ee470-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee470-217">При нажатии кнопки hello платформы Capriza плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Capriza приложения.</span><span class="sxs-lookup"><span data-stu-id="ee470-217">When you click hello Capriza Platform tile in hello Access Panel, you should get automatically signed-on tooyour Capriza application.</span></span> <span data-ttu-id="ee470-218">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee470-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee470-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ee470-219">Additional resources</span></span>

* [<span data-ttu-id="ee470-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee470-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee470-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee470-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

