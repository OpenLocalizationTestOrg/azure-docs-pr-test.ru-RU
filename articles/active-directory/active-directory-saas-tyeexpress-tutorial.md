---
title: "Руководство по интеграции Azure Active Directory с T&E Express | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="ea862-103">Руководство по интеграции Azure Active Directory с T&E Express</span><span class="sxs-lookup"><span data-stu-id="ea862-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="ea862-104">В этом учебнике вы узнаете, как toointegrate T & E экспресс-выпуск с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea862-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea862-105">Интеграция с Azure AD T & E Express предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ea862-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea862-106">Можно управлять в Azure AD, имеющего доступ tooT & E Express</span><span class="sxs-lookup"><span data-stu-id="ea862-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="ea862-107">Вы можете включить их учетные записи Azure AD пользователи tooautomatically get вошедшего tooT & E Express (Single Sign-On)</span><span class="sxs-lookup"><span data-stu-id="ea862-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea862-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="ea862-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ea862-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea862-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea862-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea862-110">Prerequisites</span></span>

<span data-ttu-id="ea862-111">tooconfigure интеграция Azure AD с T & E Express необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ea862-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="ea862-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ea862-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea862-113">подписка T&E Express с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea862-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea862-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ea862-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea862-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ea862-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea862-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="ea862-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ea862-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea862-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea862-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ea862-118">Scenario description</span></span>
<span data-ttu-id="ea862-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ea862-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea862-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ea862-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea862-121">Добавление T & E Express из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea862-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="ea862-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea862-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="ea862-123">Добавление T & E Express из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ea862-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="ea862-124">tooconfigure hello интеграции T & E Express в Azure AD, вы должны tooadd T & E Express из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea862-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea862-125">**tooadd T & E Express из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea862-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea862-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea862-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea862-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ea862-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea862-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea862-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ea862-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ea862-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ea862-133">Введите в поле поиска hello **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="ea862-133">In hello search box, type **T&E Express**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="ea862-135">В панели результатов hello выберите **T & E Express**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea862-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea862-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea862-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea862-138">В этом разделе описана настройка и проверка единого входа Azure AD в T&E Express с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea862-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea862-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в T & E Express является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea862-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="ea862-140">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в T & E Express toobe потребностей установлено.</span><span class="sxs-lookup"><span data-stu-id="ea862-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="ea862-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в T & E Express.</span><span class="sxs-lookup"><span data-stu-id="ea862-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="ea862-142">tooconfigure и теста Azure AD единого входа с T & E Express, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ea862-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea862-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ea862-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea862-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ea862-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea862-145">**[Создание тестового пользователя T & E Express](#creating-a-te-express-test-user)**  -toohave аналог Саймон Britta в T & E Express, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="ea862-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ea862-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ea862-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea862-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea862-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea862-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea862-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении T & E Express.</span><span class="sxs-lookup"><span data-stu-id="ea862-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="ea862-150">**tooconfigure Azure AD единого входа с T & E, экспресс-выпуск выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea862-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea862-151">На портале управления Azure hello на hello **T & E Express** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ea862-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ea862-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ea862-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="ea862-155">На hello **T & E Express доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea862-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="ea862-157">а.</span><span class="sxs-lookup"><span data-stu-id="ea862-157">a.</span></span> <span data-ttu-id="ea862-158">В hello **идентификатор** текстовое поле, значение типа hello как:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="ea862-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="ea862-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea862-159">b.</span></span> <span data-ttu-id="ea862-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="ea862-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea862-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="ea862-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ea862-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ea862-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ea862-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ea862-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="ea862-164">Обратитесь к [T & E Express поддержки](http://www.tyeexpress.com/contacto.aspx) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ea862-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="ea862-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea862-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="ea862-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ea862-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ea862-169">tooconfigure единого входа на **T & E быстрой** стороне, toohello входа T & E express приложения без SAML единого входа с использованием учетных данных администратора.</span><span class="sxs-lookup"><span data-stu-id="ea862-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="ea862-170">В разделе hello **администратора** щелкните **домена SAML** tooOpen hello страница "Параметры SAML".</span><span class="sxs-lookup"><span data-stu-id="ea862-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="ea862-172">Выберите hello **Activar(Activate)** меню **нет** слишком**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="ea862-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="ea862-173">В hello **метаданные поставщика удостоверений** текстовое поле, вставить hello метаданных XML, что у вас есть donwloaded из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="ea862-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="ea862-175">Щелкните hello **Guardar(Save)** кнопку Параметры toosave hello.</span><span class="sxs-lookup"><span data-stu-id="ea862-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea862-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea862-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea862-177">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ea862-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ea862-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea862-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea862-180">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ea862-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea862-182">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="ea862-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea862-184">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ea862-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea862-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea862-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea862-188">а.</span><span class="sxs-lookup"><span data-stu-id="ea862-188">a.</span></span> <span data-ttu-id="ea862-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea862-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea862-190">b.</span><span class="sxs-lookup"><span data-stu-id="ea862-190">b.</span></span> <span data-ttu-id="ea862-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea862-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea862-192">c.</span><span class="sxs-lookup"><span data-stu-id="ea862-192">c.</span></span> <span data-ttu-id="ea862-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ea862-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea862-194">d.</span><span class="sxs-lookup"><span data-stu-id="ea862-194">d.</span></span> <span data-ttu-id="ea862-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ea862-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="ea862-196">Создание тестового пользователя T&E Express</span><span class="sxs-lookup"><span data-stu-id="ea862-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="ea862-197">В порядке tooenable toolog пользователей Azure AD в T & E Express их необходимо подготовить в T & E Express.</span><span class="sxs-lookup"><span data-stu-id="ea862-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="ea862-198">В случае T&E Express подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ea862-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="ea862-199">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="ea862-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea862-200">Войдите в tooyour T & E Express сайт компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ea862-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="ea862-201">Под тегом администратора щелкните на главной странице hello tooopen пользователей пользователей.</span><span class="sxs-lookup"><span data-stu-id="ea862-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="ea862-203">На домашней странице приветствия нажмите кнопку  **+**  tooadd hello пользователей.</span><span class="sxs-lookup"><span data-stu-id="ea862-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="ea862-205">Введите все обязательные сведения hello, задаваемые в форме hello и щелкните hello сохранить сведения hello toosave кнопки.</span><span class="sxs-lookup"><span data-stu-id="ea862-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Добавление сотрудника](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea862-208">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ea862-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea862-209">В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooT & E Express.</span><span class="sxs-lookup"><span data-stu-id="ea862-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ea862-211">**tooassign tooT Britta Simon & E, экспресс-выпуск выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ea862-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea862-212">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ea862-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ea862-214">В списке приложений hello выберите **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="ea862-214">In hello applications list, select **T&E Express**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="ea862-216">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ea862-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ea862-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ea862-218">Click **Add** button.</span></span> <span data-ttu-id="ea862-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ea862-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ea862-221">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ea862-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea862-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ea862-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea862-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ea862-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea862-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ea862-224">Testing single sign-on</span></span>

<span data-ttu-id="ea862-225">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ea862-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ea862-226">При нажатии кнопки hello T & E Express плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour T & E Express приложения.</span><span class="sxs-lookup"><span data-stu-id="ea862-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea862-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ea862-227">Additional resources</span></span>

* [<span data-ttu-id="ea862-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea862-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea862-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea862-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

