---
title: "Учебник: Интеграция Azure Active Directory с BC в hello облака | Документы Microsoft"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BC в hello облака."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="1c8ff-103">Учебник: Интеграция Azure Active Directory с BC в облаке hello</span><span class="sxs-lookup"><span data-stu-id="1c8ff-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="1c8ff-104">В этом учебнике вы узнаете, как toointegrate BC в hello облака в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c8ff-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c8ff-105">Интеграция BC в hello облака в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c8ff-106">Можно управлять в Azure AD, имеющего tooBC доступа в облаке hello</span><span class="sxs-lookup"><span data-stu-id="1c8ff-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="1c8ff-107">Можно включить на пользователей tooautomatically get вошедшего tooBC в hello облака (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ff-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c8ff-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1c8ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c8ff-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c8ff-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1c8ff-110">Prerequisites</span></span>

<span data-ttu-id="1c8ff-111">tooconfigure интеграция Azure AD с BC в hello облака необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="1c8ff-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1c8ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c8ff-113">BC в hello облака единого входа в подписке включено</span><span class="sxs-lookup"><span data-stu-id="1c8ff-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c8ff-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c8ff-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c8ff-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c8ff-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c8ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c8ff-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1c8ff-118">Scenario description</span></span>
<span data-ttu-id="1c8ff-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c8ff-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c8ff-121">Добавление BC в облако из галереи hello hello</span><span class="sxs-lookup"><span data-stu-id="1c8ff-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="1c8ff-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="1c8ff-123">Добавление BC в облако из галереи hello hello</span><span class="sxs-lookup"><span data-stu-id="1c8ff-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="1c8ff-124">интеграции hello tooconfigure BC в hello облака в Azure AD, вы должны tooadd BC в hello облако из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c8ff-125">**tooadd BC в hello облака из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c8ff-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c8ff-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c8ff-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c8ff-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1c8ff-131">tooadd новое приложение, нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1c8ff-133">Введите в поле поиска hello **BC в облаке hello**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="1c8ff-135">В панели результатов hello выберите **BC в облаке hello**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c8ff-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c8ff-138">В этом разделе настройки и тестирования в Azure AD единого входа с BC в hello облака на основании тестового пользователя с именем «Britta Simon».</span><span class="sxs-lookup"><span data-stu-id="1c8ff-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c8ff-139">Для единого входа toowork Azure AD необходима tooknow какие hello пользователь аналога в BC в облаке hello является tooa пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="1c8ff-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в BC в облаке hello должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="1c8ff-141">В BC в облаке hello, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c8ff-142">tooconfigure и теста Azure AD единого входа с BC в облаке hello, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c8ff-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c8ff-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c8ff-145">**[Создание BC в hello облака тестового пользователя](#creating-a-bc-in-the-cloud-test-user)**  -toohave аналог Саймон Britta в BC в облако, которое представляет связанный toohello Azure AD пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c8ff-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c8ff-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c8ff-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c8ff-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей BC в hello облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="1c8ff-150">**tooconfigure Azure AD единого входа с BC в hello облака, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c8ff-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c8ff-151">В hello в hello портала Azure **BC в облаке hello** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1c8ff-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="1c8ff-155">На hello **BC в hello облака домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="1c8ff-157">а.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-157">a.</span></span> <span data-ttu-id="1c8ff-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="1c8ff-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="1c8ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-159">b.</span></span> <span data-ttu-id="1c8ff-160">В hello **идентификатор** текстовом поле введите URL-адрес как:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="1c8ff-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c8ff-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-161">This value is not real.</span></span> <span data-ttu-id="1c8ff-162">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1c8ff-163">Обратитесь к [BC в группа поддержки облачных клиента hello](https://www.bcinthecloud.com/supportcenter/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="1c8ff-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="1c8ff-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1c8ff-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c8ff-168">tooconfigure единого входа на **BC в облаке hello** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[BC в службу поддержки облачных hello](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="1c8ff-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="1c8ff-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1c8ff-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c8ff-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c8ff-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c8ff-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c8ff-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c8ff-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c8ff-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1c8ff-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1c8ff-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c8ff-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c8ff-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c8ff-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1c8ff-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c8ff-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1c8ff-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c8ff-184">а.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-184">a.</span></span> <span data-ttu-id="1c8ff-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c8ff-186">b.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-186">b.</span></span> <span data-ttu-id="1c8ff-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c8ff-188">c.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-188">c.</span></span> <span data-ttu-id="1c8ff-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c8ff-190">d.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-190">d.</span></span> <span data-ttu-id="1c8ff-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="1c8ff-192">Создание BC в hello облака тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1c8ff-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="1c8ff-193">В этом разделе создайте пользователя с именем Britta Simon в BC в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="1c8ff-194">Работать с [BC в группа поддержки облачных клиента hello](https://www.bcinthecloud.com/supportcenter/) для добавления пользователей hello в hello BC в hello облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="1c8ff-195">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c8ff-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1c8ff-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c8ff-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBC доступа в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1c8ff-199">**tooassign tooBC Britta Simon в hello облака, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="1c8ff-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c8ff-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1c8ff-202">В списке приложений hello выберите **BC в облаке hello**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="1c8ff-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1c8ff-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-206">Click **Add** button.</span></span> <span data-ttu-id="1c8ff-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1c8ff-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c8ff-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c8ff-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c8ff-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1c8ff-212">Testing single sign-on</span></span>

<span data-ttu-id="1c8ff-213">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="1c8ff-214">При нажатии кнопки hello BC на плитке облака hello в hello панели доступа, следует получать автоматически вошедшего tooyour BC в hello облачного приложения.</span><span class="sxs-lookup"><span data-stu-id="1c8ff-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="1c8ff-215">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c8ff-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c8ff-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1c8ff-216">Additional resources</span></span>

* [<span data-ttu-id="1c8ff-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c8ff-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c8ff-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c8ff-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

