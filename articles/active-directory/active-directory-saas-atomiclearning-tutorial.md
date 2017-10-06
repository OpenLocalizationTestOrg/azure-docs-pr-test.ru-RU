---
title: "Руководство по интеграции Azure Active Directory с Atomic Learning | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Atomic обучения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 12d7c380dbe47899eb35486c5e2a6936e8fb8b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="d97b4-103">Руководство. Интеграция Azure Active Directory с Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="d97b4-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="d97b4-104">В этом учебнике вы узнаете, как toointegrate Atomic обучения с использованием Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d97b4-104">In this tutorial, you learn how toointegrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d97b4-105">Интеграция Atomic обучения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d97b4-105">Integrating Atomic Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d97b4-106">Можно управлять в Azure AD, имеющего доступ tooAtomic обучения</span><span class="sxs-lookup"><span data-stu-id="d97b4-106">You can control in Azure AD who has access tooAtomic Learning</span></span>
- <span data-ttu-id="d97b4-107">Можно включить на пользователей tooautomatically get вошедшего tooAtomic обучения (Single Sign-On) с использованием их учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97b4-107">You can enable your users tooautomatically get signed-on tooAtomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d97b4-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d97b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d97b4-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d97b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d97b4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d97b4-110">Prerequisites</span></span>

<span data-ttu-id="d97b4-111">tooconfigure интеграция Azure AD с Atomic обучения необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="d97b4-111">tooconfigure Azure AD integration with Atomic Learning, you need hello following items:</span></span>

- <span data-ttu-id="d97b4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d97b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d97b4-113">подписка Atomic Learning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d97b4-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d97b4-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d97b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d97b4-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="d97b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d97b4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d97b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d97b4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d97b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d97b4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d97b4-118">Scenario description</span></span>
<span data-ttu-id="d97b4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d97b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d97b4-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="d97b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d97b4-121">Добавление Atomic обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d97b4-121">Adding Atomic Learning from hello gallery</span></span>
2. <span data-ttu-id="d97b4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-hello-gallery"></a><span data-ttu-id="d97b4-123">Добавление Atomic обучения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="d97b4-123">Adding Atomic Learning from hello gallery</span></span>
<span data-ttu-id="d97b4-124">tooconfigure hello интеграции Atomic обучения в Azure AD, вы должны tooadd Atomic обучения из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d97b4-124">tooconfigure hello integration of Atomic Learning into Azure AD, you need tooadd Atomic Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d97b4-125">**tooadd Atomic обучения из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="d97b4-125">**tooadd Atomic Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97b4-126">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d97b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d97b4-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d97b4-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d97b4-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="d97b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d97b4-133">Введите в поле поиска hello **Atomic обучения**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-133">In hello search box, type **Atomic Learning**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="d97b4-135">В панели результатов hello выберите **Atomic обучения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d97b4-135">In hello results panel, select **Atomic Learning**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d97b4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d97b4-138">В этом разделе описана настройка и проверка единого входа Azure AD в Atomic Learning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d97b4-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d97b4-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в атомарные обучения является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d97b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atomic Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="d97b4-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в обучении Atomic должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="d97b4-140">In other words, a link relationship between an Azure AD user and hello related user in Atomic Learning needs toobe established.</span></span>

<span data-ttu-id="d97b4-141">В атомарные обучения, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="d97b4-141">In Atomic Learning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d97b4-142">tooconfigure и теста Azure AD единого входа с Atomic обучения, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d97b4-142">tooconfigure and test Azure AD single sign-on with Atomic Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d97b4-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="d97b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d97b4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="d97b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d97b4-145">**[Создание тестового пользователя, прошедшего Atomic обучения](#creating-an-atomic-learning-test-user) ** -toohave аналог Саймон Britta Atomic обучения, которая является представлением связанного toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="d97b4-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - toohave a counterpart of Britta Simon in Atomic Learning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d97b4-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="d97b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d97b4-147">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d97b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d97b4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d97b4-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Atomic обучения.</span><span class="sxs-lookup"><span data-stu-id="d97b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="d97b4-150">**tooconfigure Azure AD единого входа с помощью Atomic обучения выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d97b4-150">**tooconfigure Azure AD single sign-on with Atomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97b4-151">В hello в hello портала Azure **Atomic обучения** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-151">In hello Azure portal, on hello **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d97b4-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="d97b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="d97b4-155">На hello **URL-адреса и домена Atomic обучения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d97b4-155">On hello **Atomic Learning Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="d97b4-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d97b4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d97b4-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="d97b4-158">This value is not real.</span></span> <span data-ttu-id="d97b4-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="d97b4-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d97b4-160">Обратитесь к [группа поддержки Atomic клиента обучения](mailto:cs@atomiclearning.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="d97b4-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="d97b4-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="d97b4-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="d97b4-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d97b4-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d97b4-165">tooconfigure единого входа на **Atomic обучения** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки Atomic обучения](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="d97b4-165">tooconfigure single sign-on on **Atomic Learning** side, you need toosend hello downloaded **Metadata XML** too[Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="d97b4-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="d97b4-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d97b4-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="d97b4-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d97b4-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="d97b4-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d97b4-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d97b4-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d97b4-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d97b4-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d97b4-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d97b4-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d97b4-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="d97b4-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97b4-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="d97b4-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d97b4-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d97b4-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="d97b4-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d97b4-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d97b4-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d97b4-182">а.</span><span class="sxs-lookup"><span data-stu-id="d97b4-182">a.</span></span> <span data-ttu-id="d97b4-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d97b4-184">b.</span><span class="sxs-lookup"><span data-stu-id="d97b4-184">b.</span></span> <span data-ttu-id="d97b4-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d97b4-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d97b4-186">c.</span><span class="sxs-lookup"><span data-stu-id="d97b4-186">c.</span></span> <span data-ttu-id="d97b4-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d97b4-188">d.</span><span class="sxs-lookup"><span data-stu-id="d97b4-188">d.</span></span> <span data-ttu-id="d97b4-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="d97b4-190">Создание тестового пользователя Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="d97b4-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="d97b4-191">В этом разделе описано, как создать пользователя Britta Simon в приложении Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="d97b4-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="d97b4-192">Приложение Atomic Learning поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d97b4-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="d97b4-193">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="d97b4-193">There is no action item for you in this section.</span></span> <span data-ttu-id="d97b4-194">Нового пользователя создается во время попытки tooaccess Atomic обучения, если он не существует еще используются hello адрес электронной почты для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d97b4-194">A new user is created during an attempt tooaccess Atomic Learning if it doesn't exist yet using hello email address for hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d97b4-195">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="d97b4-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d97b4-196">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAtomic обучения.</span><span class="sxs-lookup"><span data-stu-id="d97b4-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtomic Learning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d97b4-198">**tooassign tooAtomic Britta Simon обучения, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="d97b4-198">**tooassign Britta Simon tooAtomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d97b4-199">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d97b4-201">В списке приложений hello выберите **Atomic обучения**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-201">In hello applications list, select **Atomic Learning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="d97b4-203">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d97b4-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-205">Click **Add** button.</span></span> <span data-ttu-id="d97b4-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d97b4-208">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d97b4-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d97b4-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d97b4-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d97b4-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d97b4-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d97b4-211">Testing single sign-on</span></span>

<span data-ttu-id="d97b4-212">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="d97b4-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d97b4-213">При выборе плитки Atomic обучения hello в hello панели доступа, следует получать автоматически вошедшего tooyour Atomic обучения приложения.</span><span class="sxs-lookup"><span data-stu-id="d97b4-213">When you click hello Atomic Learning tile in hello Access Panel, you should get automatically signed-on tooyour Atomic Learning application.</span></span>
<span data-ttu-id="d97b4-214">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d97b4-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d97b4-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d97b4-215">Additional resources</span></span>

* [<span data-ttu-id="d97b4-216">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d97b4-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d97b4-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d97b4-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

