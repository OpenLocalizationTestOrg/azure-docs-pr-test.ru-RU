---
title: "Руководство по интеграции Azure Active Directory с JobScore | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6693a5fd96bfd7fbcd7197983b5f04d061970bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="bfd1d-103">Руководство по интеграции Azure Active Directory с JobScore</span><span class="sxs-lookup"><span data-stu-id="bfd1d-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="bfd1d-104">В этом учебнике вы узнаете, как toointegrate JobScore с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfd1d-104">In this tutorial, you learn how toointegrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfd1d-105">Интеграция с Azure AD JobScore предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-105">Integrating JobScore with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bfd1d-106">Можно управлять в Azure AD, имеющего доступ tooJobScore</span><span class="sxs-lookup"><span data-stu-id="bfd1d-106">You can control in Azure AD who has access tooJobScore</span></span>
- <span data-ttu-id="bfd1d-107">Можно включить на пользователей tooautomatically get вошедшего tooJobScore (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd1d-107">You can enable your users tooautomatically get signed-on tooJobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfd1d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="bfd1d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bfd1d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfd1d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfd1d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bfd1d-110">Prerequisites</span></span>

<span data-ttu-id="bfd1d-111">tooconfigure интеграция Azure AD с JobScore требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-111">tooconfigure Azure AD integration with JobScore, you need hello following items:</span></span>

- <span data-ttu-id="bfd1d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bfd1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfd1d-113">подписка JobScore с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfd1d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfd1d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfd1d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfd1d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfd1d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfd1d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bfd1d-118">Scenario description</span></span>
<span data-ttu-id="bfd1d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfd1d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfd1d-121">Добавление JobScore из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bfd1d-121">Adding JobScore from hello gallery</span></span>
2. <span data-ttu-id="bfd1d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-hello-gallery"></a><span data-ttu-id="bfd1d-123">Добавление JobScore из галереи hello</span><span class="sxs-lookup"><span data-stu-id="bfd1d-123">Adding JobScore from hello gallery</span></span>
<span data-ttu-id="bfd1d-124">tooconfigure hello интеграции JobScore в Azure AD, вы должны tooadd JobScore из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-124">tooconfigure hello integration of JobScore into Azure AD, you need tooadd JobScore from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bfd1d-125">**tooadd JobScore из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfd1d-125">**tooadd JobScore from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfd1d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfd1d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bfd1d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bfd1d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bfd1d-133">Введите в поле поиска hello **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-133">In hello search box, type **JobScore**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="bfd1d-135">В панели результатов hello выберите **JobScore**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-135">In hello results panel, select **JobScore**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfd1d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd1d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfd1d-138">В этом разделе описана настройка и проверка единого входа Azure AD в JobScore с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfd1d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в JobScore является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JobScore is tooa user in Azure AD.</span></span> <span data-ttu-id="bfd1d-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в JobScore должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-140">In other words, a link relationship between an Azure AD user and hello related user in JobScore needs toobe established.</span></span>

<span data-ttu-id="bfd1d-141">В JobScore, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-141">In JobScore, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bfd1d-142">tooconfigure и теста Azure AD единого входа с JobScore, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-142">tooconfigure and test Azure AD single sign-on with JobScore, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bfd1d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bfd1d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfd1d-145">**[Создание тестового пользователя JobScore](#creating-a-jobscore-test-user)**  -toohave аналог Саймон Britta в JobScore, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - toohave a counterpart of Britta Simon in JobScore that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfd1d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfd1d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfd1d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd1d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfd1d-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении JobScore.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="bfd1d-150">**tooconfigure Azure AD единого входа с JobScore, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfd1d-150">**tooconfigure Azure AD single sign-on with JobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfd1d-151">В hello в hello портала Azure **JobScore** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-151">In hello Azure portal, on hello **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bfd1d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="bfd1d-155">На hello **URL-адреса и домена JobScore** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-155">On hello **JobScore Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="bfd1d-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="bfd1d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bfd1d-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-158">This value is not real.</span></span> <span data-ttu-id="bfd1d-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bfd1d-160">Обратитесь к [группа поддержки клиента JobScore](mailto:support@jobscore.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-160">Contact [JobScore Client support team](mailto:support@jobscore.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="bfd1d-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="bfd1d-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bfd1d-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bfd1d-165">tooconfigure единого входа на **JobScore** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[JobScore поддержки](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="bfd1d-165">tooconfigure single sign-on on **JobScore** side, you need toosend hello downloaded **Metadata XML** too[JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="bfd1d-166">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="bfd1d-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bfd1d-167">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bfd1d-168">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bfd1d-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfd1d-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfd1d-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfd1d-170">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bfd1d-172">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfd1d-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfd1d-173">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfd1d-175">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfd1d-177">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="bfd1d-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfd1d-179">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="bfd1d-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfd1d-181">а.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-181">a.</span></span> <span data-ttu-id="bfd1d-182">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfd1d-183">b.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-183">b.</span></span> <span data-ttu-id="bfd1d-184">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfd1d-185">c.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-185">c.</span></span> <span data-ttu-id="bfd1d-186">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bfd1d-187">d.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-187">d.</span></span> <span data-ttu-id="bfd1d-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="bfd1d-189">Создание тестового пользователя JobScore</span><span class="sxs-lookup"><span data-stu-id="bfd1d-189">Creating a JobScore test user</span></span>

<span data-ttu-id="bfd1d-190">В этом разделе описано, как создать пользователя Britta Simon в приложении JobScore.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="bfd1d-191">Работать с [JobScore поддержки](mailto:support@jobscore.com) tooadd hello пользователей на платформе JobScore hello.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-191">Work with [JobScore support team](mailto:support@jobscore.com) tooadd hello users in hello JobScore platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bfd1d-192">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="bfd1d-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bfd1d-193">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJobScore доступа.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobScore.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bfd1d-195">**tooassign tooJobScore Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="bfd1d-195">**tooassign Britta Simon tooJobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="bfd1d-196">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bfd1d-198">В списке приложений hello выберите **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-198">In hello applications list, select **JobScore**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="bfd1d-200">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bfd1d-202">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-202">Click **Add** button.</span></span> <span data-ttu-id="bfd1d-203">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bfd1d-205">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bfd1d-206">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfd1d-207">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfd1d-208">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bfd1d-208">Testing single sign-on</span></span>

<span data-ttu-id="bfd1d-209">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bfd1d-210">При нажатии кнопки hello JobScore плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour JobScore приложения.</span><span class="sxs-lookup"><span data-stu-id="bfd1d-210">When you click hello JobScore tile in hello Access Panel, you should get automatically signed-on tooyour JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bfd1d-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bfd1d-211">Additional resources</span></span>

* [<span data-ttu-id="bfd1d-212">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfd1d-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfd1d-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfd1d-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

