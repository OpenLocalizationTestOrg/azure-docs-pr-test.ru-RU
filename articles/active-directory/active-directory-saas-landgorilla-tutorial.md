---
title: "Руководство по интеграции Azure Active Directory с Land Gorilla Client | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Gorilla Земли."
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
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="ad5d9-103">Руководство по интеграции Azure Active Directory с Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="ad5d9-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="ad5d9-104">В этом учебнике вы узнаете, как toointegrate клиента Gorilla Земли с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad5d9-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad5d9-105">Интеграция клиента Gorilla Земли с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad5d9-106">Можно управлять в Azure AD, имеющего доступ tooLand Gorilla клиента</span><span class="sxs-lookup"><span data-stu-id="ad5d9-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="ad5d9-107">Ваш пользователей tooautomatically get вошедшего tooLand Gorilla клиента (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad5d9-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad5d9-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="ad5d9-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ad5d9-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad5d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ad5d9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ad5d9-110">Prerequisites</span></span>

<span data-ttu-id="ad5d9-111">tooconfigure интеграция Azure AD с Земли Gorilla клиента требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="ad5d9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ad5d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad5d9-113">подписка Land Gorilla Client с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ad5d9-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ad5d9-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad5d9-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ad5d9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad5d9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ad5d9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ad5d9-118">Scenario description</span></span>
<span data-ttu-id="ad5d9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad5d9-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad5d9-121">Добавление клиента Gorilla Земли из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ad5d9-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="ad5d9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad5d9-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="ad5d9-123">Добавление клиента Gorilla Земли из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ad5d9-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="ad5d9-124">tooconfigure hello интеграции Земли Gorilla клиента в Azure AD, вы должны tooadd Земли Gorilla клиента из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad5d9-125">**tooadd Земли Gorilla клиента из коллекции hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ad5d9-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad5d9-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad5d9-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad5d9-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ad5d9-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ad5d9-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ad5d9-133">Введите в поле поиска hello **Земли Gorilla клиента**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="ad5d9-135">В панели результатов hello выберите **клиента Gorilla Земли**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad5d9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad5d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad5d9-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Land Gorilla Client с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad5d9-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в клиенте Gorilla Земли является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="ad5d9-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в клиенте Gorilla Земли должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="ad5d9-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в клиенте Gorilla Земли.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="ad5d9-142">tooconfigure и теста Azure AD единого входа с клиента Gorilla земли, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad5d9-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad5d9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с ограниченной группе.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="ad5d9-145">**[Создание тестового пользователя Gorilla Земли](#creating-a-land-gorilla-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ad5d9-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad5d9-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad5d9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad5d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad5d9-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении клиента Gorilla Земли.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="ad5d9-150">**tooconfigure Azure AD единого входа с клиента Gorilla земли, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ad5d9-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad5d9-151">На портале управления Azure hello на hello **клиента Gorilla Земли** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ad5d9-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="ad5d9-155">На hello **URL-адреса и домена клиента Gorilla Земли** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="ad5d9-157">а.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-157">a.</span></span> <span data-ttu-id="ad5d9-158">В hello **идентификатор** текстовое значение hello типа с помощью одного из hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="ad5d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-159">b.</span></span> <span data-ttu-id="ad5d9-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, с помощью одного из hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="ad5d9-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ad5d9-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ad5d9-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="ad5d9-164">Обратитесь к [клиента Gorilla Земли команды](https://www.landgorilla.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="ad5d9-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="ad5d9-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ad5d9-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="ad5d9-169">tooget единого входа: Завершение настройки приложения в конце Gorilla земли, обратитесь к [группа поддержки клиента Gorilla Земли](https://www.landgorilla.com/support/) и предоставить им загружаются hello **«метаданные в формате XML** файла.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad5d9-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad5d9-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad5d9-171">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ad5d9-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ad5d9-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad5d9-174">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad5d9-176">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad5d9-178">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad5d9-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad5d9-182">а.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-182">a.</span></span> <span data-ttu-id="ad5d9-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad5d9-184">b.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-184">b.</span></span> <span data-ttu-id="ad5d9-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad5d9-186">c.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-186">c.</span></span> <span data-ttu-id="ad5d9-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad5d9-188">d.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-188">d.</span></span> <span data-ttu-id="ad5d9-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="ad5d9-190">Создание тестового пользователя Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="ad5d9-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="ad5d9-191">Можно работать с [группа поддержки Gorilla Земли](https://www.landgorilla.com/support/) tooadd hello пользователей на платформе Gorilla Земли hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad5d9-192">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ad5d9-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad5d9-193">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooLand Gorilla клиента.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ad5d9-195">**tooassign tooLand Britta Simon Gorilla клиента, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="ad5d9-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad5d9-196">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ad5d9-198">В списке приложений hello выберите **Земли Gorilla клиента**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="ad5d9-200">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ad5d9-202">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-202">Click **Add** button.</span></span> <span data-ttu-id="ad5d9-203">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ad5d9-205">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad5d9-206">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad5d9-207">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ad5d9-208">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ad5d9-208">Testing single sign-on</span></span>

<span data-ttu-id="ad5d9-209">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad5d9-210">Если щелкнуть плитку клиента Gorilla Земли hello в hello панели доступа, вы должны получить tooyour автоматически подписан на землю Gorilla клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ad5d9-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ad5d9-211">Additional resources</span></span>

* [<span data-ttu-id="ad5d9-212">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad5d9-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad5d9-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad5d9-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
