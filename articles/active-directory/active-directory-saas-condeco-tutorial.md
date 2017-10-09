---
title: "Учебник. Интеграция Azure Active Directory с Condeco | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Condeco."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4601c17d-ad93-4865-8885-b378c4bbe82b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 20c57ff0466c28d4fb69f73bc8b5a479715eba0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-condeco"></a><span data-ttu-id="7f6ac-103">Учебник. Интеграция Azure Active Directory с Concur</span><span class="sxs-lookup"><span data-stu-id="7f6ac-103">Tutorial: Azure Active Directory integration with Condeco</span></span>

<span data-ttu-id="7f6ac-104">В этом учебнике вы узнаете, как toointegrate Condeco с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-104">In this tutorial, you learn how toointegrate Condeco with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f6ac-105">Интеграция с Azure AD Condeco предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-105">Integrating Condeco with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f6ac-106">Можно управлять в Azure AD, имеющего доступ tooCondeco</span><span class="sxs-lookup"><span data-stu-id="7f6ac-106">You can control in Azure AD who has access tooCondeco</span></span>
- <span data-ttu-id="7f6ac-107">Можно включить на пользователей tooautomatically get вошедшего tooCondeco (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f6ac-107">You can enable your users tooautomatically get signed-on tooCondeco (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f6ac-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7f6ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7f6ac-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f6ac-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f6ac-110">Prerequisites</span></span>

<span data-ttu-id="7f6ac-111">tooconfigure интеграция Azure AD с Condeco требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-111">tooconfigure Azure AD integration with Condeco, you need hello following items:</span></span>

- <span data-ttu-id="7f6ac-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7f6ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f6ac-113">подписка с поддержкой единого входа Condeco.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-113">A Condeco single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f6ac-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f6ac-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f6ac-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f6ac-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f6ac-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7f6ac-118">Scenario description</span></span>
<span data-ttu-id="7f6ac-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f6ac-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f6ac-121">Добавление Condeco из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f6ac-121">Adding Condeco from hello gallery</span></span>
2. <span data-ttu-id="7f6ac-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f6ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-condeco-from-hello-gallery"></a><span data-ttu-id="7f6ac-123">Добавление Condeco из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7f6ac-123">Adding Condeco from hello gallery</span></span>
<span data-ttu-id="7f6ac-124">tooconfigure hello интеграции Condeco в Azure AD, вы должны tooadd Condeco из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-124">tooconfigure hello integration of Condeco into Azure AD, you need tooadd Condeco from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f6ac-125">**tooadd Condeco из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f6ac-125">**tooadd Condeco from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f6ac-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f6ac-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f6ac-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7f6ac-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7f6ac-133">Введите в поле поиска hello **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-133">In hello search box, type **Condeco**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_search.png)

5. <span data-ttu-id="7f6ac-135">В панели результатов hello выберите **Condeco**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-135">In hello results panel, select **Condeco**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f6ac-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f6ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f6ac-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Condeco для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-138">In this section, you configure and test Azure AD single sign-on with Condeco based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7f6ac-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Condeco является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Condeco is tooa user in Azure AD.</span></span> <span data-ttu-id="7f6ac-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Condeco должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-140">In other words, a link relationship between an Azure AD user and hello related user in Condeco needs toobe established.</span></span>

<span data-ttu-id="7f6ac-141">В Condeco, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-141">In Condeco, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f6ac-142">tooconfigure и теста Azure AD единого входа с Condeco, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-142">tooconfigure and test Azure AD single sign-on with Condeco, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f6ac-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f6ac-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f6ac-145">**[Создание тестового пользователя Condeco](#creating-a-condeco-test-user)**  -toohave аналог Саймон Britta в Condeco, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-145">**[Creating a Condeco test user](#creating-a-condeco-test-user)** - toohave a counterpart of Britta Simon in Condeco that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f6ac-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f6ac-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f6ac-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f6ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f6ac-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Condeco.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Condeco application.</span></span>

<span data-ttu-id="7f6ac-150">**tooconfigure Azure AD единого входа с Condeco, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f6ac-150">**tooconfigure Azure AD single sign-on with Condeco, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f6ac-151">В hello в hello портала Azure **Condeco** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-151">In hello Azure portal, on hello **Condeco** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7f6ac-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_samlbase.png)

3. <span data-ttu-id="7f6ac-155">На hello **URL-адреса и домена Condeco** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-155">On hello **Condeco Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_url.png)

    <span data-ttu-id="7f6ac-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.condecosoftware.com`</span><span class="sxs-lookup"><span data-stu-id="7f6ac-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.condecosoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f6ac-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-158">This value is not real.</span></span> <span data-ttu-id="7f6ac-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7f6ac-160">Обратитесь к [группа поддержки клиента Condeco](mailTo:supportna@condecosoftware.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-160">Contact [Condeco Client support team](mailTo:supportna@condecosoftware.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="7f6ac-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_certificate.png) 

5. <span data-ttu-id="7f6ac-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7f6ac-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7f6ac-165">tooconfigure единого входа на **Condeco** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Condeco поддержки](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-165">tooconfigure single sign-on on **Condeco** side, you need toosend hello downloaded **Metadata XML** too[Condeco support team](mailTo:supportna@condecosoftware.com).</span></span> <span data-ttu-id="7f6ac-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7f6ac-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7f6ac-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f6ac-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f6ac-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f6ac-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f6ac-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f6ac-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f6ac-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7f6ac-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f6ac-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f6ac-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f6ac-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f6ac-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7f6ac-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f6ac-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f6ac-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f6ac-182">а.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-182">a.</span></span> <span data-ttu-id="7f6ac-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f6ac-184">b.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-184">b.</span></span> <span data-ttu-id="7f6ac-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f6ac-186">c.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-186">c.</span></span> <span data-ttu-id="7f6ac-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7f6ac-188">d.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-188">d.</span></span> <span data-ttu-id="7f6ac-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-189">Click **Create**.</span></span>
 
### <a name="creating-a-condeco-test-user"></a><span data-ttu-id="7f6ac-190">Создание тестового пользователя Condeco</span><span class="sxs-lookup"><span data-stu-id="7f6ac-190">Creating a Condeco test user</span></span>

<span data-ttu-id="7f6ac-191">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Condeco.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-191">hello objective of this section is toocreate a user called Britta Simon in Condeco.</span></span> <span data-ttu-id="7f6ac-192">Приложение Condeco поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-192">Condeco supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7f6ac-193">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-193">There is no action item for you in this section.</span></span> <span data-ttu-id="7f6ac-194">Новый пользователь создается во время попытки tooaccess Condeco, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-194">A new user is created during an attempt tooaccess Condeco if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7f6ac-195">Если требуется toocreate пользователя вручную, необходимо toocontact hello [Condeco поддержки](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-195">If you need toocreate a user manually, you need toocontact hello [Condeco support team](mailTo:supportna@condecosoftware.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7f6ac-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7f6ac-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7f6ac-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCondeco доступа.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCondeco.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7f6ac-199">**tooassign tooCondeco Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7f6ac-199">**tooassign Britta Simon tooCondeco, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f6ac-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7f6ac-202">В списке приложений hello выберите **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-202">In hello applications list, select **Condeco**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_app.png) 

3. <span data-ttu-id="7f6ac-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7f6ac-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-206">Click **Add** button.</span></span> <span data-ttu-id="7f6ac-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7f6ac-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f6ac-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f6ac-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f6ac-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7f6ac-212">Testing single sign-on</span></span>

<span data-ttu-id="7f6ac-213">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f6ac-214">При нажатии кнопки hello Condeco плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Condeco приложения.</span><span class="sxs-lookup"><span data-stu-id="7f6ac-214">When you click hello Condeco tile in hello Access Panel, you should get automatically signed-on tooyour Condeco application.</span></span>
<span data-ttu-id="7f6ac-215">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f6ac-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f6ac-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f6ac-216">Additional resources</span></span>

* [<span data-ttu-id="7f6ac-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f6ac-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f6ac-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f6ac-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_203.png

