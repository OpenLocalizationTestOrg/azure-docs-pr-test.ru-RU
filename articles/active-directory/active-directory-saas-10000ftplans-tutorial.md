---
title: "Руководство по интеграции Azure Active Directory с 10,000ft Plans | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и 10 000 футов планы."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="1f3aa-103">Учебник. Интеграция Azure Active Directory с 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="1f3aa-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="1f3aa-104">В этом учебнике вы узнаете, как toointegrate 10 000 футов планов с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f3aa-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f3aa-105">Интеграция 10 000 футов планов с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f3aa-106">Можно управлять в Azure AD, имеющего доступ too10, 000 футов планов</span><span class="sxs-lookup"><span data-stu-id="1f3aa-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="1f3aa-107">Можно включить на пользователей tooautomatically get вошедшего too10, планы 000 футов (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3aa-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f3aa-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f3aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f3aa-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f3aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f3aa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f3aa-110">Prerequisites</span></span>

<span data-ttu-id="1f3aa-111">tooconfigure интеграция Azure AD с 10 000 футов планов требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="1f3aa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="1f3aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f3aa-113">подписка 10,000ft Plans с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f3aa-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f3aa-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f3aa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f3aa-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f3aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f3aa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1f3aa-118">Scenario description</span></span>
<span data-ttu-id="1f3aa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f3aa-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f3aa-121">Добавление 10 000 футов планы из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1f3aa-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="1f3aa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="1f3aa-123">Добавление 10 000 футов планы из галереи hello</span><span class="sxs-lookup"><span data-stu-id="1f3aa-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="1f3aa-124">tooconfigure hello Интеграция планов 10 000 футов в Azure AD, необходимо tooadd 10 000 футов планы из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f3aa-125">**tooadd 10 000 футов планы из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f3aa-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f3aa-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f3aa-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f3aa-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="1f3aa-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="1f3aa-133">Введите в поле поиска hello **планы 10 000 футов**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="1f3aa-135">В панели результатов hello выберите **планы 10 000 футов**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f3aa-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f3aa-138">В этом разделе описана настройка и проверка единого входа Azure AD в 10,000ft Plans с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f3aa-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в 10 000 футов планах является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="1f3aa-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в 10 000 футов планы должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="1f3aa-141">В 10 000 футов планов, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1f3aa-142">tooconfigure и теста Azure AD единого входа с 10 000 футов планы, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f3aa-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f3aa-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f3aa-145">**[Создание 10 000 футов планы тестовый пользователь](#creating-a-10000ft-plans-test-user)**  -toohave аналог Саймон Britta в 10 000 футов планы, связанные представление toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f3aa-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f3aa-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f3aa-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f3aa-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении планы 10 000 футов.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="1f3aa-150">**tooconfigure Azure AD единого входа с 10 000 футов планов, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f3aa-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f3aa-151">В hello в hello портала Azure **планы 10 000 футов** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="1f3aa-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="1f3aa-155">На hello **10 000 футов планы домена и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="1f3aa-157">а.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-157">a.</span></span> <span data-ttu-id="1f3aa-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="1f3aa-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="1f3aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-159">b.</span></span> <span data-ttu-id="1f3aa-160">В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="1f3aa-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f3aa-161">Здравствуйте, значение для **идентификатор** отличается, если у вас есть пользовательский домен.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="1f3aa-162">Обратитесь к [10 000 футов планы поддержки](https://www.10000ft.com/plans/support) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="1f3aa-163">На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="1f3aa-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="1f3aa-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f3aa-167">На hello **10 000 футов планы конфигурации** щелкните **Настройка планов 10 000 футов** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1f3aa-168">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="1f3aa-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="1f3aa-170">tooconfigure единого входа на **планы 10 000 футов** стороны, необходимо загрузить hello toosend **Certificate(Raw), URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[ Группа поддержки планы 10 000 футов](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="1f3aa-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="1f3aa-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="1f3aa-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f3aa-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f3aa-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f3aa-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f3aa-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3aa-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f3aa-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="1f3aa-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="1f3aa-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f3aa-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f3aa-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f3aa-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="1f3aa-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f3aa-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="1f3aa-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f3aa-186">а.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-186">a.</span></span> <span data-ttu-id="1f3aa-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f3aa-188">b.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-188">b.</span></span> <span data-ttu-id="1f3aa-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f3aa-190">c.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-190">c.</span></span> <span data-ttu-id="1f3aa-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f3aa-192">d.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-192">d.</span></span> <span data-ttu-id="1f3aa-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="1f3aa-194">Создание тестового пользователя 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="1f3aa-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="1f3aa-195">Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в планах 10 000 футов.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="1f3aa-196">Приложение 10,000ft Plans поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1f3aa-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-197">There is no action item for you in this section.</span></span> <span data-ttu-id="1f3aa-198">Новый пользователь создается во время попытки tooaccess 10 000 футов планы, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f3aa-199">Если требуется toocreate пользователя вручную, необходимо toocontact hello [10 000 футов планы поддержки](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="1f3aa-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f3aa-200">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="1f3aa-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f3aa-201">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа too10, планы 000 футов.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="1f3aa-203">**tooassign too10 Britta Simon планы 000 футов выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="1f3aa-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f3aa-204">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="1f3aa-206">В списке приложений hello выберите **планы 10 000 футов**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="1f3aa-208">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="1f3aa-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-210">Click **Add** button.</span></span> <span data-ttu-id="1f3aa-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="1f3aa-213">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f3aa-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f3aa-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f3aa-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="1f3aa-216">Testing single sign-on</span></span>

<span data-ttu-id="1f3aa-217">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="1f3aa-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="1f3aa-218">При нажатии кнопки hello 10 000 футов, планы плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на 10 000 футов планы приложения.</span><span class="sxs-lookup"><span data-stu-id="1f3aa-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="1f3aa-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1f3aa-219">Additional resources</span></span>

* [<span data-ttu-id="1f3aa-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f3aa-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f3aa-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f3aa-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

