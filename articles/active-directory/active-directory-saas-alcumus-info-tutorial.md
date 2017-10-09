---
title: "Руководство. Интеграция Azure Active Directory с Alcumus Info Exchange | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Alcumus Info Exchange."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 4ef9f4d654b6c451db44f929bdad1016304168b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="cfdbe-103">Учебник. Интеграция Azure Active Directory с Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cfdbe-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="cfdbe-104">В этом учебнике вы узнаете, как toointegrate Alcumus сведения обмена с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfdbe-104">In this tutorial, you learn how toointegrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfdbe-105">Интеграция Exchange Alcumus сведения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="cfdbe-105">Integrating Alcumus Info Exchange with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfdbe-106">Можно управлять в Azure AD, имеющего доступ tooAlcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cfdbe-106">You can control in Azure AD who has access tooAlcumus Info Exchange</span></span>
- <span data-ttu-id="cfdbe-107">Ваш пользователей tooautomatically get вошедшего tooAlcumus Exchange Info (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdbe-107">You can enable your users tooautomatically get signed-on tooAlcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfdbe-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cfdbe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cfdbe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfdbe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfdbe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cfdbe-110">Prerequisites</span></span>

<span data-ttu-id="cfdbe-111">tooconfigure интеграция Azure AD с Exchange Alcumus сведения, необходимые hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-111">tooconfigure Azure AD integration with Alcumus Info Exchange, you need hello following items:</span></span>

- <span data-ttu-id="cfdbe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cfdbe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfdbe-113">подписка Alcumus Info Exchange с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfdbe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfdbe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="cfdbe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfdbe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfdbe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfdbe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfdbe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cfdbe-118">Scenario description</span></span>
<span data-ttu-id="cfdbe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfdbe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="cfdbe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfdbe-121">Добавление Alcumus Info Exchange из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cfdbe-121">Adding Alcumus Info Exchange from hello gallery</span></span>
2. <span data-ttu-id="cfdbe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdbe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-hello-gallery"></a><span data-ttu-id="cfdbe-123">Добавление Alcumus Info Exchange из галереи hello</span><span class="sxs-lookup"><span data-stu-id="cfdbe-123">Adding Alcumus Info Exchange from hello gallery</span></span>
<span data-ttu-id="cfdbe-124">tooconfigure hello интеграции Exchange Alcumus сведения в Azure AD, вы должны tooadd Alcumus Info Exchange из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-124">tooconfigure hello integration of Alcumus Info Exchange into Azure AD, you need tooadd Alcumus Info Exchange from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfdbe-125">**tooadd Alcumus Exchange сведения из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="cfdbe-125">**tooadd Alcumus Info Exchange from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdbe-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfdbe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfdbe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cfdbe-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cfdbe-133">Введите в поле поиска hello **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-133">In hello search box, type **Alcumus Info Exchange**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="cfdbe-135">В панели результатов hello, выберите **Exchange сведения Alcumus**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-135">In hello results panel, select **Alcumus Info Exchange**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfdbe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdbe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfdbe-138">В этом разделе описана настройка и проверка единого входа Azure AD в Alcumus Info Exchange с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cfdbe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Alcumus Info Exchange является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Alcumus Info Exchange is tooa user in Azure AD.</span></span> <span data-ttu-id="cfdbe-140">Иными словами связи между пользователя Azure AD и hello связанных пользователей в Exchange сведения Alcumus должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-140">In other words, a link relationship between an Azure AD user and hello related user in Alcumus Info Exchange needs toobe established.</span></span>

<span data-ttu-id="cfdbe-141">В Alcumus Info Exchange, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-141">In Alcumus Info Exchange, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfdbe-142">tooconfigure и теста Azure AD единого входа с Exchange Alcumus сведения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-142">tooconfigure and test Azure AD single sign-on with Alcumus Info Exchange, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfdbe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfdbe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfdbe-145">**[Создание тестового пользователя, прошедшего Exchange сведения Alcumus](#creating-an-alcumus-info-exchange-test-user)**  -toohave аналог Саймон Britta в Exchange Alcumus сведения, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - toohave a counterpart of Britta Simon in Alcumus Info Exchange that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfdbe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfdbe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfdbe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdbe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfdbe-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="cfdbe-150">**tooconfigure Azure AD единого входа с Exchange Alcumus сведения, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cfdbe-150">**tooconfigure Azure AD single sign-on with Alcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdbe-151">В hello в hello портала Azure **Exchange сведения Alcumus** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-151">In hello Azure portal, on hello **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cfdbe-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="cfdbe-155">На hello **URL-адреса и домена Exchange сведения Alcumus** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cfdbe-155">On hello **Alcumus Info Exchange Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="cfdbe-157">а.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-157">a.</span></span> <span data-ttu-id="cfdbe-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="cfdbe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="cfdbe-159">b.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-159">b.</span></span> <span data-ttu-id="cfdbe-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="cfdbe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cfdbe-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-161">These values are not real.</span></span> <span data-ttu-id="cfdbe-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cfdbe-163">Обратитесь к [группа поддержки Exchange сведения Alcumus](mailto:helpdesk@alcumusgroup.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) tooget these values.</span></span>
 
4. <span data-ttu-id="cfdbe-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="cfdbe-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="cfdbe-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfdbe-168">tooconfigure единого входа на **Alcumus Info Exchange** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки Exchange сведения Alcumus](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="cfdbe-168">tooconfigure single sign-on on **Alcumus Info Exchange** side, you need toosend hello downloaded **Metadata XML** too[Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="cfdbe-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="cfdbe-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfdbe-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfdbe-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfdbe-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfdbe-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfdbe-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfdbe-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cfdbe-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="cfdbe-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdbe-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfdbe-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfdbe-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="cfdbe-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfdbe-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="cfdbe-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfdbe-184">а.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-184">a.</span></span> <span data-ttu-id="cfdbe-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfdbe-186">b.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-186">b.</span></span> <span data-ttu-id="cfdbe-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfdbe-188">c.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-188">c.</span></span> <span data-ttu-id="cfdbe-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cfdbe-190">d.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-190">d.</span></span> <span data-ttu-id="cfdbe-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="cfdbe-192">Создание тестового пользователя Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cfdbe-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="cfdbe-193">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Alcumus обмена сведения.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-193">hello objective of this section is toocreate a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="cfdbe-194">toocreate пользователя с именем в Exchange Alcumus сведения, обратитесь в службу hello Саймон Britta [группа поддержки Exchange сведения Alcumus](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="cfdbe-194">toocreate a user called Britta Simon in Alcumus Info Exchange, Contact hello [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cfdbe-195">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="cfdbe-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cfdbe-196">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAlcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAlcumus Info Exchange.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cfdbe-198">**tooassign tooAlcumus Britta Simon Info Exchange, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="cfdbe-198">**tooassign Britta Simon tooAlcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfdbe-199">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cfdbe-201">В списке приложений hello выберите **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-201">In hello applications list, select **Alcumus Info Exchange**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="cfdbe-203">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cfdbe-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-205">Click **Add** button.</span></span> <span data-ttu-id="cfdbe-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cfdbe-208">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfdbe-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfdbe-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfdbe-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cfdbe-211">Testing single sign-on</span></span>

<span data-ttu-id="cfdbe-212">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="cfdbe-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="cfdbe-213">При выборе плитки Alcumus Info Exchange hello в hello панели доступа, вы должны получить приложения автоматически вошедшего tooyour Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="cfdbe-213">When you click hello Alcumus Info Exchange tile in hello Access Panel, you should get automatically signed-on tooyour Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfdbe-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cfdbe-214">Additional resources</span></span>

* [<span data-ttu-id="cfdbe-215">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfdbe-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfdbe-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cfdbe-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

