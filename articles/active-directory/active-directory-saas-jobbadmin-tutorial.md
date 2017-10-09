---
title: "Руководство по интеграции Azure Active Directory с Jobbadmin | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0796abd2934c0f94648b2c11e7fdf69304f835c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="89118-103">Руководство по интеграции Azure Active Directory с Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="89118-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="89118-104">В этом учебнике вы узнаете, как toointegrate Jobbadmin с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89118-104">In this tutorial, you learn how toointegrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89118-105">Интеграция с Azure AD Jobbadmin предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="89118-105">Integrating Jobbadmin with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89118-106">Можно управлять в Azure AD, имеющего доступ tooJobbadmin</span><span class="sxs-lookup"><span data-stu-id="89118-106">You can control in Azure AD who has access tooJobbadmin</span></span>
- <span data-ttu-id="89118-107">Можно включить на пользователей tooautomatically get вошедшего tooJobbadmin (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="89118-107">You can enable your users tooautomatically get signed-on tooJobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89118-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="89118-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="89118-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89118-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89118-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89118-110">Prerequisites</span></span>

<span data-ttu-id="89118-111">tooconfigure интеграция Azure AD с Jobbadmin требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="89118-111">tooconfigure Azure AD integration with Jobbadmin, you need hello following items:</span></span>

- <span data-ttu-id="89118-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="89118-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89118-113">подписка на Jobbadmin с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="89118-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89118-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="89118-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89118-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="89118-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89118-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="89118-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89118-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89118-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89118-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="89118-118">Scenario description</span></span>
<span data-ttu-id="89118-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="89118-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89118-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="89118-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89118-121">Добавление Jobbadmin из галереи hello</span><span class="sxs-lookup"><span data-stu-id="89118-121">Adding Jobbadmin from hello gallery</span></span>
2. <span data-ttu-id="89118-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="89118-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-hello-gallery"></a><span data-ttu-id="89118-123">Добавление Jobbadmin из галереи hello</span><span class="sxs-lookup"><span data-stu-id="89118-123">Adding Jobbadmin from hello gallery</span></span>
<span data-ttu-id="89118-124">tooconfigure hello интеграции Jobbadmin в Azure AD, вы должны tooadd Jobbadmin из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="89118-124">tooconfigure hello integration of Jobbadmin into Azure AD, you need tooadd Jobbadmin from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89118-125">**tooadd Jobbadmin из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="89118-125">**tooadd Jobbadmin from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89118-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="89118-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89118-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="89118-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89118-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="89118-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="89118-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="89118-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="89118-133">Введите в поле поиска hello **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="89118-133">In hello search box, type **Jobbadmin**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="89118-135">В панели результатов hello выберите **Jobbadmin**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="89118-135">In hello results panel, select **Jobbadmin**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89118-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="89118-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89118-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jobbadmin с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89118-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="89118-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jobbadmin является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89118-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobbadmin is tooa user in Azure AD.</span></span> <span data-ttu-id="89118-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Jobbadmin должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="89118-140">In other words, a link relationship between an Azure AD user and hello related user in Jobbadmin needs toobe established.</span></span>

<span data-ttu-id="89118-141">В Jobbadmin, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="89118-141">In Jobbadmin, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="89118-142">tooconfigure и теста Azure AD единого входа с Jobbadmin, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="89118-142">tooconfigure and test Azure AD single sign-on with Jobbadmin, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89118-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="89118-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89118-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="89118-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89118-145">**[Создание тестового пользователя Jobbadmin](#creating-a-jobbadmin-test-user)**  -toohave аналог Саймон Britta в Jobbadmin, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="89118-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - toohave a counterpart of Britta Simon in Jobbadmin that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89118-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="89118-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89118-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="89118-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89118-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="89118-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89118-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="89118-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="89118-150">**tooconfigure Azure AD единого входа с Jobbadmin, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="89118-150">**tooconfigure Azure AD single sign-on with Jobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="89118-151">В hello в hello портала Azure **Jobbadmin** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="89118-151">In hello Azure portal, on hello **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="89118-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="89118-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="89118-155">На hello **URL-адреса и домена Jobbadmin** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="89118-155">On hello **Jobbadmin Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="89118-157">а.</span><span class="sxs-lookup"><span data-stu-id="89118-157">a.</span></span> <span data-ttu-id="89118-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="89118-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="89118-159">b.</span><span class="sxs-lookup"><span data-stu-id="89118-159">b.</span></span> <span data-ttu-id="89118-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="89118-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="89118-161">c.</span><span class="sxs-lookup"><span data-stu-id="89118-161">c.</span></span> <span data-ttu-id="89118-162">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="89118-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89118-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="89118-163">These values are not real.</span></span> <span data-ttu-id="89118-164">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="89118-164">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="89118-165">Обратитесь к [группа поддержки клиента Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="89118-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget these values.</span></span> 
 


4. <span data-ttu-id="89118-166">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="89118-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="89118-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="89118-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89118-170">tooconfigure единого входа на **Jobbadmin** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Jobbadmin поддержки](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="89118-170">tooconfigure single sign-on on **Jobbadmin** side, you need toosend hello downloaded **Metadata XML** too[Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="89118-171">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="89118-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="89118-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="89118-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89118-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="89118-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89118-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89118-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89118-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="89118-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="89118-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="89118-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="89118-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="89118-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89118-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="89118-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89118-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="89118-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89118-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="89118-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89118-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="89118-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89118-187">а.</span><span class="sxs-lookup"><span data-stu-id="89118-187">a.</span></span> <span data-ttu-id="89118-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89118-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89118-189">b.</span><span class="sxs-lookup"><span data-stu-id="89118-189">b.</span></span> <span data-ttu-id="89118-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89118-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89118-191">c.</span><span class="sxs-lookup"><span data-stu-id="89118-191">c.</span></span> <span data-ttu-id="89118-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="89118-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89118-193">d.</span><span class="sxs-lookup"><span data-stu-id="89118-193">d.</span></span> <span data-ttu-id="89118-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="89118-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="89118-195">Создание тестового пользователя Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="89118-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="89118-196">Пользователи toolog tooenable Azure AD в tooJobbadmin, их необходимо подготовить в Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="89118-196">tooenable Azure AD users toolog in tooJobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="89118-197">Обратитесь в службу [Jobbadmin поддержки](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget пользователей hello, добавленных с их стороны.</span><span class="sxs-lookup"><span data-stu-id="89118-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) tooget hello users added on their side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89118-198">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="89118-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89118-199">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJobbadmin доступа.</span><span class="sxs-lookup"><span data-stu-id="89118-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobbadmin.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="89118-201">**tooassign tooJobbadmin Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="89118-201">**tooassign Britta Simon tooJobbadmin, perform hello following steps:**</span></span>

1. <span data-ttu-id="89118-202">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="89118-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="89118-204">В списке приложений hello выберите **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="89118-204">In hello applications list, select **Jobbadmin**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="89118-206">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="89118-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="89118-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="89118-208">Click **Add** button.</span></span> <span data-ttu-id="89118-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="89118-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="89118-211">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="89118-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89118-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="89118-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89118-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="89118-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89118-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="89118-214">Testing single sign-on</span></span>

<span data-ttu-id="89118-215">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="89118-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89118-216">При нажатии кнопки hello Jobbadmin плитки в панели доступа hello, должно появиться страница входа Jobbadmin приложения.</span><span class="sxs-lookup"><span data-stu-id="89118-216">When you click hello Jobbadmin tile in hello Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="89118-217">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89118-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89118-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="89118-218">Additional resources</span></span>

* [<span data-ttu-id="89118-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89118-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89118-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89118-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

