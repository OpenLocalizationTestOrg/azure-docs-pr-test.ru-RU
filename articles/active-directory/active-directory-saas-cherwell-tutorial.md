---
title: "Учебник. Интеграция Azure Active Directory с Cherwell | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cherwell."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: a67b3d346a6f7b43a7e87fb4d9c533f9363f2e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="37a5b-103">Руководство. Интеграция Azure Active Directory с Cherwell</span><span class="sxs-lookup"><span data-stu-id="37a5b-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="37a5b-104">В этом учебнике вы узнаете, как toointegrate Cherwell с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37a5b-104">In this tutorial, you learn how toointegrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37a5b-105">Интеграция Cherwell с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="37a5b-105">Integrating Cherwell with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="37a5b-106">Можно управлять в Azure AD, имеющего доступ tooCherwell</span><span class="sxs-lookup"><span data-stu-id="37a5b-106">You can control in Azure AD who has access tooCherwell</span></span>
- <span data-ttu-id="37a5b-107">Можно включить на пользователей tooautomatically get вошедшего tooCherwell (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a5b-107">You can enable your users tooautomatically get signed-on tooCherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37a5b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="37a5b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="37a5b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37a5b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37a5b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="37a5b-110">Prerequisites</span></span>

<span data-ttu-id="37a5b-111">tooconfigure интеграция Azure AD с Cherwell требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="37a5b-111">tooconfigure Azure AD integration with Cherwell, you need hello following items:</span></span>

- <span data-ttu-id="37a5b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="37a5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37a5b-113">подписка Cherwell с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="37a5b-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37a5b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="37a5b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37a5b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="37a5b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37a5b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="37a5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37a5b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37a5b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37a5b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="37a5b-118">Scenario description</span></span>
<span data-ttu-id="37a5b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="37a5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37a5b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="37a5b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37a5b-121">Добавление Cherwell из галереи hello</span><span class="sxs-lookup"><span data-stu-id="37a5b-121">Adding Cherwell from hello gallery</span></span>
2. <span data-ttu-id="37a5b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a5b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-hello-gallery"></a><span data-ttu-id="37a5b-123">Добавление Cherwell из галереи hello</span><span class="sxs-lookup"><span data-stu-id="37a5b-123">Adding Cherwell from hello gallery</span></span>
<span data-ttu-id="37a5b-124">tooconfigure hello интеграции Cherwell в Azure AD, вы должны tooadd Cherwell из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="37a5b-124">tooconfigure hello integration of Cherwell into Azure AD, you need tooadd Cherwell from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37a5b-125">**tooadd Cherwell из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37a5b-125">**tooadd Cherwell from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37a5b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="37a5b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37a5b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="37a5b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="37a5b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="37a5b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="37a5b-133">Введите в поле поиска hello **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-133">In hello search box, type **Cherwell**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="37a5b-135">В панели результатов hello выберите **Cherwell**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="37a5b-135">In hello results panel, select **Cherwell**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37a5b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a5b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37a5b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Cherwell с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37a5b-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="37a5b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Cherwell является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37a5b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cherwell is tooa user in Azure AD.</span></span> <span data-ttu-id="37a5b-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Cherwell должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="37a5b-140">In other words, a link relationship between an Azure AD user and hello related user in Cherwell needs toobe established.</span></span>

<span data-ttu-id="37a5b-141">В Cherwell, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="37a5b-141">In Cherwell, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="37a5b-142">tooconfigure и теста Azure AD единого входа с Cherwell, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="37a5b-142">tooconfigure and test Azure AD single sign-on with Cherwell, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37a5b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="37a5b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37a5b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="37a5b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37a5b-145">**[Создание тестового пользователя Cherwell](#creating-a-cherwell-test-user)**  -toohave аналог Саймон Britta в Cherwell, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="37a5b-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - toohave a counterpart of Britta Simon in Cherwell that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="37a5b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="37a5b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37a5b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="37a5b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37a5b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a5b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37a5b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Cherwell.</span><span class="sxs-lookup"><span data-stu-id="37a5b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="37a5b-150">**Azure AD tooconfigure единого входа с Cherwell, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37a5b-150">**tooconfigure Azure AD single sign-on with Cherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="37a5b-151">В hello в hello портала Azure **Cherwell** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-151">In hello Azure portal, on hello **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="37a5b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="37a5b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="37a5b-155">На hello **URL-адреса и домена Cherwell** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="37a5b-155">On hello **Cherwell Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="37a5b-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="37a5b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37a5b-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="37a5b-158">This value is not real.</span></span> <span data-ttu-id="37a5b-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="37a5b-159">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="37a5b-160">Обратитесь к [поддержки cherwell](https://csm.cherwell.com/contact) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="37a5b-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) tooget this value.</span></span>
 
4. <span data-ttu-id="37a5b-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="37a5b-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="37a5b-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="37a5b-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37a5b-165">На hello **конфигурации Cherwell** щелкните **Настройка Cherwell** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="37a5b-165">On hello **Cherwell Configuration** section, click **Configure Cherwell** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="37a5b-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="37a5b-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="37a5b-168">tooconfigure единого входа на **Cherwell** стороны, необходимо загрузить hello toosend **сертификата (Base64)**, **SAML единого входа URL-адрес службы**, и  **Идентификатор сущности SAML** слишком[поддержки cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="37a5b-168">tooconfigure single sign-on on **Cherwell** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="37a5b-169">Поддержка cherwell имеет toodo hello фактическую настройку единого входа.</span><span class="sxs-lookup"><span data-stu-id="37a5b-169">Your Cherwell support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="37a5b-170">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="37a5b-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="37a5b-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="37a5b-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="37a5b-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="37a5b-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="37a5b-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37a5b-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37a5b-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a5b-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="37a5b-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37a5b-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="37a5b-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37a5b-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37a5b-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="37a5b-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37a5b-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37a5b-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="37a5b-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37a5b-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="37a5b-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37a5b-186">а.</span><span class="sxs-lookup"><span data-stu-id="37a5b-186">a.</span></span> <span data-ttu-id="37a5b-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37a5b-188">b.</span><span class="sxs-lookup"><span data-stu-id="37a5b-188">b.</span></span> <span data-ttu-id="37a5b-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37a5b-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37a5b-190">c.</span><span class="sxs-lookup"><span data-stu-id="37a5b-190">c.</span></span> <span data-ttu-id="37a5b-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="37a5b-192">d.</span><span class="sxs-lookup"><span data-stu-id="37a5b-192">d.</span></span> <span data-ttu-id="37a5b-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="37a5b-194">Создание тестового пользователя Cherwell</span><span class="sxs-lookup"><span data-stu-id="37a5b-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="37a5b-195">Пользователи toolog tooenable Azure AD в tooCherwell, их необходимо подготовить в Cherwell.</span><span class="sxs-lookup"><span data-stu-id="37a5b-195">tooenable Azure AD users toolog in tooCherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="37a5b-196">В случае hello Cherwell, учетные записи пользователей hello должны toobe, созданные вашей [поддержки cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="37a5b-196">In hello case of Cherwell, hello user accounts need toobe created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="37a5b-197">Можно использовать любые другие Cherwell пользователя средства создания учетных записей или API, предоставленные Cherwell tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="37a5b-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37a5b-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="37a5b-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="37a5b-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCherwell доступа.</span><span class="sxs-lookup"><span data-stu-id="37a5b-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCherwell.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="37a5b-201">**tooassign tooCherwell Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="37a5b-201">**tooassign Britta Simon tooCherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="37a5b-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="37a5b-204">В списке приложений hello выберите **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-204">In hello applications list, select **Cherwell**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="37a5b-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="37a5b-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-208">Click **Add** button.</span></span> <span data-ttu-id="37a5b-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="37a5b-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="37a5b-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="37a5b-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37a5b-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="37a5b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37a5b-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="37a5b-214">Testing single sign-on</span></span>

<span data-ttu-id="37a5b-215">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="37a5b-215">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="37a5b-216">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37a5b-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37a5b-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="37a5b-217">Additional resources</span></span>

* [<span data-ttu-id="37a5b-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37a5b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37a5b-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37a5b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

