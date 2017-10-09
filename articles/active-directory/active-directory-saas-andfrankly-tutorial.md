---
title: "Руководство. Интеграция Azure Active Directory с &frankly | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и & честно говоря."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="39dcf-103">Руководство. Интеграция Azure Active Directory с &frankly</span><span class="sxs-lookup"><span data-stu-id="39dcf-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="39dcf-104">В этом учебнике вы узнаете, как toointegrate & честно говоря с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39dcf-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39dcf-105">Интеграция & честно говоря в Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="39dcf-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39dcf-106">Можно управлять в Azure AD, который имеет доступ слишком & честно говоря</span><span class="sxs-lookup"><span data-stu-id="39dcf-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="39dcf-107">Можно включить пользователей tooautomatically получить вошедшего слишком & честно говоря (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="39dcf-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39dcf-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="39dcf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39dcf-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39dcf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39dcf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="39dcf-110">Prerequisites</span></span>

<span data-ttu-id="39dcf-111">Интеграция Azure AD tooconfigure с & честно говоря, необходимы hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="39dcf-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="39dcf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="39dcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39dcf-113">подписка &frankly с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="39dcf-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39dcf-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="39dcf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39dcf-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="39dcf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39dcf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="39dcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39dcf-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39dcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39dcf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="39dcf-118">Scenario description</span></span>
<span data-ttu-id="39dcf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="39dcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39dcf-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="39dcf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39dcf-121">Добавление & честно говоря из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39dcf-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="39dcf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39dcf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="39dcf-123">Добавление & честно говоря из галереи hello</span><span class="sxs-lookup"><span data-stu-id="39dcf-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="39dcf-124">Интеграция hello tooconfigure & честно говоря в Azure AD, необходимо tooadd & честно говоря из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="39dcf-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39dcf-125">**tooadd & честно говоря из галереи hello, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="39dcf-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39dcf-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="39dcf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39dcf-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39dcf-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="39dcf-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="39dcf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="39dcf-133">Введите в поле поиска hello **& честно говоря**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-133">In hello search box, type **&frankly**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="39dcf-135">В панели результатов hello выберите **& честно говоря**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39dcf-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39dcf-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39dcf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39dcf-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение &frankly с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39dcf-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="39dcf-139">Для единого входа toowork Azure AD необходима tooknow какой hello пользователя аналога в & честно говоря — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39dcf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="39dcf-140">Другими словами ссылка связь между пользователя Azure AD и связанных пользователей hello в & честно говоря установлено toobe потребностей.</span><span class="sxs-lookup"><span data-stu-id="39dcf-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="39dcf-141">В & честно говоря, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="39dcf-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39dcf-142">tooconfigure и Azure AD единого входа с & тестирования честно говоря, вы должны hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="39dcf-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39dcf-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="39dcf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39dcf-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="39dcf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39dcf-145">**[Создание & честно говоря тестового пользователя](#creating-a-frankly-test-user)**  -toohave аналог Саймон Britta в & честно говоря, связанный toohello представление пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39dcf-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39dcf-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="39dcf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39dcf-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39dcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39dcf-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="39dcf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39dcf-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ваш & честно говоря приложения.</span><span class="sxs-lookup"><span data-stu-id="39dcf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="39dcf-150">**Azure AD tooconfigure один вход с & честно говоря, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="39dcf-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="39dcf-151">В hello в hello портала Azure **& честно говоря** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="39dcf-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="39dcf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="39dcf-155">На hello **& честно говоря URL-адреса и домена** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="39dcf-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="39dcf-157">а.</span><span class="sxs-lookup"><span data-stu-id="39dcf-157">a.</span></span> <span data-ttu-id="39dcf-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="39dcf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="39dcf-159">b.</span><span class="sxs-lookup"><span data-stu-id="39dcf-159">b.</span></span> <span data-ttu-id="39dcf-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="39dcf-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="39dcf-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="39dcf-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="39dcf-162">При необходимости приложение hello tooconfigure в **SP** инициировал режим:</span><span class="sxs-lookup"><span data-stu-id="39dcf-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="39dcf-164">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="39dcf-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="39dcf-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="39dcf-165">These values are not real.</span></span> <span data-ttu-id="39dcf-166">Обновить эти значения с hello фактический идентификатор входа и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="39dcf-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="39dcf-167">Обратитесь к [andfrankly поддержки](mailto:help@andfrankly.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="39dcf-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="39dcf-168">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="39dcf-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="39dcf-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="39dcf-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="39dcf-172">tooconfigure единого входа на **& честно говоря** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[andfrankly поддержки](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="39dcf-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="39dcf-173">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="39dcf-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39dcf-174">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="39dcf-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39dcf-175">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39dcf-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39dcf-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="39dcf-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="39dcf-177">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="39dcf-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="39dcf-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39dcf-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39dcf-180">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="39dcf-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39dcf-182">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39dcf-184">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="39dcf-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39dcf-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="39dcf-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39dcf-188">а.</span><span class="sxs-lookup"><span data-stu-id="39dcf-188">a.</span></span> <span data-ttu-id="39dcf-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39dcf-190">b.</span><span class="sxs-lookup"><span data-stu-id="39dcf-190">b.</span></span> <span data-ttu-id="39dcf-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39dcf-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39dcf-192">c.</span><span class="sxs-lookup"><span data-stu-id="39dcf-192">c.</span></span> <span data-ttu-id="39dcf-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39dcf-194">d.</span><span class="sxs-lookup"><span data-stu-id="39dcf-194">d.</span></span> <span data-ttu-id="39dcf-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="39dcf-196">Создание тестового пользователя приложения &frankly</span><span class="sxs-lookup"><span data-stu-id="39dcf-196">Creating a &frankly test user</span></span>

<span data-ttu-id="39dcf-197">В этом разделе описано, как создать пользователя Britta Simon в приложении &frankly.</span><span class="sxs-lookup"><span data-stu-id="39dcf-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="39dcf-198">Работать с [andfrankly поддержки](mailto:help@andfrankly.com) tooadd пользователей hello в Привет & честно говоря платформы.</span><span class="sxs-lookup"><span data-stu-id="39dcf-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39dcf-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="39dcf-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39dcf-200">В этом разделе, предоставление доступа слишком & честно говоря включен toouse Britta Simon Azure единого входа.</span><span class="sxs-lookup"><span data-stu-id="39dcf-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="39dcf-202">**tooassign Britta Simon слишком & честно говоря, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="39dcf-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="39dcf-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="39dcf-205">В списке приложений hello выберите **& честно говоря**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-205">In hello applications list, select **&frankly**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="39dcf-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="39dcf-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-209">Click **Add** button.</span></span> <span data-ttu-id="39dcf-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="39dcf-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="39dcf-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39dcf-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39dcf-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="39dcf-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39dcf-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="39dcf-215">Testing single sign-on</span></span>

<span data-ttu-id="39dcf-216">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="39dcf-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="39dcf-217">Когда щелкните hello & честно говоря плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на & честно говоря приложения</span><span class="sxs-lookup"><span data-stu-id="39dcf-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39dcf-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="39dcf-218">Additional resources</span></span>

* [<span data-ttu-id="39dcf-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39dcf-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39dcf-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39dcf-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

