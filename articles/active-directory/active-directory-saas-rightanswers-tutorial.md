---
title: "Руководство по интеграции Azure Active Directory с RightAnswers | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и RightAnswers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 745e7ed5a13291afeed8f48a595e95b27d4b0e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="012a6-103">Учебник. Интеграция Azure Active Directory с RightAnswers</span><span class="sxs-lookup"><span data-stu-id="012a6-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="012a6-104">В этом учебнике вы узнаете, как toointegrate RightAnswers с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="012a6-104">In this tutorial, you learn how toointegrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="012a6-105">Интеграция с Azure AD RightAnswers предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="012a6-105">Integrating RightAnswers with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="012a6-106">Можно управлять в Azure AD, имеющего доступ tooRightAnswers</span><span class="sxs-lookup"><span data-stu-id="012a6-106">You can control in Azure AD who has access tooRightAnswers</span></span>
- <span data-ttu-id="012a6-107">Можно включить на пользователей tooautomatically get вошедшего tooRightAnswers (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="012a6-107">You can enable your users tooautomatically get signed-on tooRightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="012a6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="012a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="012a6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="012a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="012a6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="012a6-110">Prerequisites</span></span>

<span data-ttu-id="012a6-111">tooconfigure интеграция Azure AD с RightAnswers требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="012a6-111">tooconfigure Azure AD integration with RightAnswers, you need hello following items:</span></span>

- <span data-ttu-id="012a6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="012a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="012a6-113">подписка RightAnswers с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="012a6-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="012a6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="012a6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="012a6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="012a6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="012a6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="012a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="012a6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="012a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="012a6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="012a6-118">Scenario description</span></span>
<span data-ttu-id="012a6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="012a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="012a6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="012a6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="012a6-121">Добавление RightAnswers из галереи hello</span><span class="sxs-lookup"><span data-stu-id="012a6-121">Adding RightAnswers from hello gallery</span></span>
2. <span data-ttu-id="012a6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="012a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-hello-gallery"></a><span data-ttu-id="012a6-123">Добавление RightAnswers из галереи hello</span><span class="sxs-lookup"><span data-stu-id="012a6-123">Adding RightAnswers from hello gallery</span></span>
<span data-ttu-id="012a6-124">tooconfigure hello интеграции RightAnswers в Azure AD, вы должны tooadd RightAnswers из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="012a6-124">tooconfigure hello integration of RightAnswers into Azure AD, you need tooadd RightAnswers from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="012a6-125">**tooadd RightAnswers из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="012a6-125">**tooadd RightAnswers from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="012a6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="012a6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="012a6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="012a6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="012a6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="012a6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="012a6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="012a6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="012a6-133">Введите в поле поиска hello **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="012a6-133">In hello search box, type **RightAnswers**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="012a6-135">В панели результатов hello выберите **RightAnswers**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="012a6-135">In hello results panel, select **RightAnswers**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="012a6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="012a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="012a6-138">В этом разделе описана настройка и проверка единого входа Azure AD в RightAnswers с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="012a6-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="012a6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в RightAnswers является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="012a6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RightAnswers is tooa user in Azure AD.</span></span> <span data-ttu-id="012a6-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в RightAnswers должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="012a6-140">In other words, a link relationship between an Azure AD user and hello related user in RightAnswers needs toobe established.</span></span>

<span data-ttu-id="012a6-141">В RightAnswers, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="012a6-141">In RightAnswers, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="012a6-142">tooconfigure и теста Azure AD единого входа с RightAnswers, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="012a6-142">tooconfigure and test Azure AD single sign-on with RightAnswers, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="012a6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="012a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="012a6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="012a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="012a6-145">**[Создание тестового пользователя RightAnswers](#creating-a-rightanswers-test-user)**  -toohave аналог Саймон Britta в RightAnswers, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="012a6-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - toohave a counterpart of Britta Simon in RightAnswers that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="012a6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="012a6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="012a6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="012a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="012a6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="012a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="012a6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="012a6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="012a6-150">**tooconfigure Azure AD единого входа с RightAnswers, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="012a6-150">**tooconfigure Azure AD single sign-on with RightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="012a6-151">В hello в hello портала Azure **RightAnswers** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="012a6-151">In hello Azure portal, on hello **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="012a6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="012a6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="012a6-155">На hello **URL-адреса и домена RightAnswers** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="012a6-155">On hello **RightAnswers Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="012a6-157">а.</span><span class="sxs-lookup"><span data-stu-id="012a6-157">a.</span></span> <span data-ttu-id="012a6-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="012a6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="012a6-159">b.</span><span class="sxs-lookup"><span data-stu-id="012a6-159">b.</span></span> <span data-ttu-id="012a6-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="012a6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="012a6-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="012a6-161">These values are not real.</span></span> <span data-ttu-id="012a6-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="012a6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="012a6-163">Обратитесь к [группа поддержки клиента RightAnswers](https://www.rightanswers.com/contact-us/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="012a6-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="012a6-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="012a6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="012a6-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="012a6-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="012a6-168">tooconfigure единого входа на **RightAnswers** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[RightAnswers поддержки](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="012a6-168">tooconfigure single sign-on on **RightAnswers** side, you need toosend hello downloaded **Metadata XML** too[RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="012a6-169">Сотрудники службы поддержки RightAnswers имеет toodo hello фактическую настройку единого входа.</span><span class="sxs-lookup"><span data-stu-id="012a6-169">Your RightAnswers support team has toodo hello actual SSO configuration.</span></span>
    ><span data-ttu-id="012a6-170">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="012a6-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="012a6-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="012a6-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="012a6-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="012a6-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="012a6-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="012a6-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="012a6-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="012a6-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="012a6-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="012a6-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="012a6-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="012a6-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="012a6-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="012a6-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="012a6-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="012a6-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="012a6-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="012a6-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="012a6-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="012a6-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="012a6-186">а.</span><span class="sxs-lookup"><span data-stu-id="012a6-186">a.</span></span> <span data-ttu-id="012a6-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="012a6-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="012a6-188">b.</span><span class="sxs-lookup"><span data-stu-id="012a6-188">b.</span></span> <span data-ttu-id="012a6-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="012a6-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="012a6-190">c.</span><span class="sxs-lookup"><span data-stu-id="012a6-190">c.</span></span> <span data-ttu-id="012a6-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="012a6-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="012a6-192">d.</span><span class="sxs-lookup"><span data-stu-id="012a6-192">d.</span></span> <span data-ttu-id="012a6-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="012a6-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="012a6-194">Создание тестового пользователя RightAnswers</span><span class="sxs-lookup"><span data-stu-id="012a6-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="012a6-195">Пользователи toolog tooenable Azure AD в tooRightAnswers, их необходимо подготовить в RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="012a6-195">tooenable Azure AD users toolog in tooRightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="012a6-196">В случае RightAnswers подготовка выполняется автоматически, так что вам не нужно ничего делать.</span><span class="sxs-lookup"><span data-stu-id="012a6-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="012a6-197">Пользователи создаются автоматически при необходимости hello первой единого входа попытки.</span><span class="sxs-lookup"><span data-stu-id="012a6-197">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="012a6-198">Можно использовать любые другие RightAnswers пользователя средства создания учетных записей или интерфейсы API, предоставляемые RightAnswers tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="012a6-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="012a6-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="012a6-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="012a6-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRightAnswers доступа.</span><span class="sxs-lookup"><span data-stu-id="012a6-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightAnswers.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="012a6-202">**tooassign tooRightAnswers Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="012a6-202">**tooassign Britta Simon tooRightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="012a6-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="012a6-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="012a6-205">В списке приложений hello выберите **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="012a6-205">In hello applications list, select **RightAnswers**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="012a6-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="012a6-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="012a6-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="012a6-209">Click **Add** button.</span></span> <span data-ttu-id="012a6-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="012a6-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="012a6-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="012a6-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="012a6-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="012a6-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="012a6-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="012a6-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="012a6-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="012a6-215">Testing single sign-on</span></span>

<span data-ttu-id="012a6-216">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="012a6-216">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="012a6-217">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="012a6-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="012a6-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="012a6-218">Additional resources</span></span>

* [<span data-ttu-id="012a6-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="012a6-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="012a6-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="012a6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

